# На шляху до високодоступного Node-RED

Це перекладена стаття [Toward Highly Available Node-RED](https://flowforge.com/blog/2023/02/highly-available-node-red/) від ZJ van de Weg

Протягом останніх кількох місяців ми провели багато сесій для ознайомлення з продуктами, і тема, яка постійно виникає, це "HA Node-RED"(Highly Available Node-RED). Усе програмне забезпечення матиме збої, а HA (висока доступність) має на меті дозволити обробку робочого навантаження незалежно від цього. Є чимало міркувань, які часто не розглядаються під час викликів щодо створення продукту, я збираюся обговорити деякі з них у цій статті.

Коли моя посада була інженером-програмістом, мені пощастило розробити та впровадити систему високої доступності. Це неймовірно складне та корисне завдання для будь-якого програмного інженера. Як тема, вона вивчається під час отримання ступеня бакалавра комп’ютерних наук, магістра та навіть доктора філософії. Коли мені поставили завдання створити систему високої доступності, мені знадобився добрий місяць, щоб визначити, якими були наші цілі та що ми готові обміняти на потрібні властивості. Це може бути додаткове обладнання, інженерні години, а також організаційні проблеми. А поки що зосередимося на перших двох.

Почнемо з означення мети: зменшити вплив екземпляра Node-RED, який не відповідає з певної причини. У багатьох випадках вимірюється MTTR (Mean Time To Recovery, середній час до відновлення). Якщо, наприклад, збій апаратного забезпечення призведе до зупинки екземпляра, а час на виявлення дорівнює нулю, швидше за все, для відновлення знадобиться кілька годин. Більшість роботи з відновлення також виконується вручну, і знання про те, як відновити, зазвичай є [племінними знаннями](https://en.wikipedia.org/wiki/Tribal_knowledge). Якщо потрібна особа на місці, доступне необхідне обладнання, ви зберегли чудові резервні копії та можете негайно розгорнути нове обладнання без підтримки інших функцій, ви можете досягти MTTR у 120 хвилин!

### Середній час відновлення 5-10 хвилин 

Що потрібно, щоб зробити це, скажімо, до 10 хвилин? По-перше, впровадження FlowForge тут дуже допоможе. FlowForge можна встановити локально, або ви можете скористатися нашою керованою хмарою. Програмне забезпечення те саме, якщо локальне встановлення використовує наш метод [встановлення Kubernetes](https://flowforge.com/docs/install/kubernetes/).

Ключовим моментом інсталяції є той факт, що апаратний рівень узагальнено як парк. Виявлення збоїв включено в інсталяцію, і це дуже швидко. Порівнюючи це з більшістю нинішніх систем оповіщення, зазвичай це різниця між ніччю та днем. Крім того, щоб значно скоротити час відновлення, існує вимога зробити програмне забезпечення відповідальним за всю процедуру. Втручання людини приводить до суттєвого сповільнення.

Щоб скоротити MTTR до 5 хвилин, потрібно або автоматично зробити обладнання доступним для парку, або зробити його надлишковим (доступно більше обладнання, ніж потрібно в будь-який момент). У разі збою апаратного забезпечення FlowForge налаштовано таким чином, щоб усі екземпляри Node-RED, які є KIA, були замінені. Зменшення часу відновлення приблизно до 5 хвилин. Для багатьох випадків використання MTTR 5 хвилин є *достатнім*.

### MTTR за долі хвилини

Щоб зменшити MTTR до часу менше хвилини, або, насмілюся сказати, менше 10 секунд, нам потрібно буде збільшити кількість запущених екземплярів Node-RED. Почнемо з гарячого резервування. Це означає, що є запущений екземпляр Node-RED з потоками, точно такими ж, як і інший, готовий взятися за роботу, коли на першому виникне збій. Зауважте, що це не є естафетою, естафета не передається від одного Node-RED до іншого. Хоча деякі дані та повідомлення можуть бути втрачені, можна за лічені секунди перенаправити все робоче навантаження з Node-RED, що вийшов з ладу на гарячий резерв. Люди зазвичай спостерігають за гарячим резервом лише через кілька хвилин після того, як вони замінюють несправний екземпляр.

### Долі секунди!

Перш ніж ця публікація перетвориться на теоретичну вправу, нам дійсно потрібно зрозуміти, які компроміси прийнятні для вас. Є [Теорема CAP](https://en.wikipedia.org/wiki/CAP_theorem), яка стверджує, що потрібні 3 гарантії: Consistency (узгодженість), Availability (доступність) і Partition Tolerance (допуск до розділення). Ви можете вибрати лише два. Під час виробництва лінію ніколи не можна зупиняти за причини збою програмного забезпечення, тому доступність є найважливішою. Питання в тому, що буде далі? Чи це означає узгодженість, що всі 3 екземпляри мають однакове уявлення про глобальний стан? Або, можливо, Partition Tolerance, де для кожного екземпляра життєво важливо мати можливість передбачити заплановану дію, навіть якщо він не може повідомити інші?

Незалежно від того, які 2 гарантії ви виберете, їх вирішення залежатиме від інженерного вибору в пошуках чудового рішення високої доступності.

### Дорожня карта

З FlowForge v1.4, випущеним у лютому 2023 року, досягається 5-хвилинний середній час відновлення для всіх потоків, що виконуються локально, тобто в кластері. Для досягнення цієї віхи потрібен ваш внесок! Я хотів би поговорити про ваші виклики, [виберіть часовий проміжок, щоб обговорити свої вимоги](https://meetings-eu1.hubspot.com/zeger-jan)!