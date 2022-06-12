#### ReplyKeyboardMarkup

<https://core.telegram.org/bots/api/#replykeyboardmarkup>

This object represents a [custom keyboard](https://core.telegram.org/bots#keyboards) with reply options (see [Introduction to bots](https://core.telegram.org/bots#keyboards) for details and examples).

| Field                   | Type                                                         | Description                                                  |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| keyboard                | Array of Array of [KeyboardButton](https://core.telegram.org/bots/api/#keyboardbutton) | Array of button rows, each represented by an Array of [KeyboardButton](https://core.telegram.org/bots/api/#keyboardbutton) objects |
| resize_keyboard         | Boolean                                                      | *Optional*. Requests clients to resize the keyboard  vertically for optimal fit (e.g., make the keyboard smaller if there are just two rows of buttons). Defaults to *false*, in which case the custom keyboard is always of the same height as the app's standard keyboard. |
| one_time_keyboard       | Boolean                                                      | *Optional*. Requests clients to hide the keyboard as soon as  it's been used. The keyboard will still be available, but clients will  automatically display the usual letter-keyboard in the chat – the user  can press a special button in the input field to see the custom keyboard again. Defaults to *false*. |
| input_field_placeholder | String                                                       | *Optional*. The placeholder to be shown in the input field when the keyboard is active; 1-64 characters |
| selective               | Boolean                                                      | *Optional*. Use this parameter if you want to show the keyboard to specific users only. Targets: 1) users that are @mentioned in the *text* of the [Message](https://core.telegram.org/bots/api/#message) object; 2) if the bot's message is a reply (has *reply_to_message_id*), sender of the original message.  *Example:* A user requests to change the bot's language, bot replies to the  request with a keyboard to select the new language. Other users in the  group don't see the keyboard. |

#### KeyboardButton

This object represents one button of the reply keyboard. For simple text buttons *String* can be used instead of this object to specify text of the button. Optional fields *request_contact*, *request_location*, and *request_poll* are mutually exclusive.

| Field            | Type                                                         | Description                                                  |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| text             | String                                                       | Text of the button. If none of the optional fields are used, it will be sent as a message when the button is pressed |
| request_contact  | Boolean                                                      | *Optional*. If *True*, the user's phone number will be sent as a contact when the button is pressed. Available in private chats only |
| request_location | Boolean                                                      | *Optional*. If *True*, the user's current location will be sent when the button is pressed. Available in private chats only |
| request_poll     | [KeyboardButtonPollType](https://core.telegram.org/bots/api/#keyboardbuttonpolltype) | *Optional*. If specified, the user will be asked to create a  poll and send it to the bot when the button is pressed. Available in  private chats only |

**Note:** *request_contact* and *request_location* options will only work in Telegram versions released after 9 April, 2016. Older clients will display *unsupported message*.
**Note:** *request_poll* option will only work in Telegram versions released after 23 January, 2020. Older clients will display *unsupported message*.

#### KeyboardButtonPollType

This object represents type of a poll, which is allowed to be created and sent when the corresponding button is pressed.

| Field | Type   | Description                                                  |
| ----- | ------ | ------------------------------------------------------------ |
| type  | String | *Optional*. If *quiz* is passed, the user will be allowed to create only polls in the quiz mode. If *regular* is passed, only regular polls will be allowed. Otherwise, the user will be allowed to create a poll of any type. |

#### ReplyKeyboardRemove

Upon receiving a message with this object, Telegram clients will  remove the current custom keyboard and display the default  letter-keyboard. By default, custom keyboards are displayed until a new  keyboard is sent by a bot. An exception is made for one-time keyboards  that are hidden immediately after the user presses a button (see [ReplyKeyboardMarkup](https://core.telegram.org/bots/api/#replykeyboardmarkup)).

| Field           | Type    | Description                                                  |
| --------------- | ------- | ------------------------------------------------------------ |
| remove_keyboard | True    | Requests clients to remove the custom keyboard (user will not be  able to summon this keyboard; if you want to hide the keyboard from  sight but keep it accessible, use *one_time_keyboard* in [ReplyKeyboardMarkup](https://core.telegram.org/bots/api/#replykeyboardmarkup)) |
| selective       | Boolean | *Optional*. Use this parameter if you want to remove the keyboard for specific users only. Targets: 1) users that are @mentioned in the *text* of the [Message](https://core.telegram.org/bots/api/#message) object; 2) if the bot's message is a reply (has *reply_to_message_id*), sender of the original message.  *Example:* A user votes in a poll, bot returns confirmation message in reply to  the vote and removes the keyboard for that user, while still showing the keyboard with poll options to users who haven't voted yet. |

#### InlineKeyboardMarkup

This object represents an [inline keyboard](https://core.telegram.org/bots#inline-keyboards-and-on-the-fly-updating) that appears right next to the message it belongs to.

| Field           | Type                                                         | Description                                                  |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| inline_keyboard | Array of Array of [InlineKeyboardButton](https://core.telegram.org/bots/api/#inlinekeyboardbutton) | Array of button rows, each represented by an Array of [InlineKeyboardButton](https://core.telegram.org/bots/api/#inlinekeyboardbutton) objects |

**Note:** This will only work in Telegram versions released after 9 April, 2016. Older clients will display *unsupported message*.

#### InlineKeyboardButton

This object represents one button of an inline keyboard. You **must** use exactly one of the optional fields.

| Field                            | Type                                                         | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| text                             | String                                                       | Label text on the button                                     |
| url                              | String                                                       | *Optional*. HTTP or tg:// url to be opened when button is pressed |
| login_url                        | [LoginUrl](https://core.telegram.org/bots/api/#loginurl)     | *Optional*. An HTTP URL used to automatically authorize the user. Can be used as a replacement for the [Telegram Login Widget](https://core.telegram.org/widgets/login). |
| callback_data                    | String                                                       | *Optional*. Data to be sent in a [callback query](https://core.telegram.org/bots/api/#callbackquery) to the bot when button is pressed, 1-64 bytes |
| switch_inline_query              | String                                                       | *Optional*. If set, pressing the button will prompt the user  to select one of their chats, open that chat and insert the bot's  username and the specified inline query in the input field. Can be  empty, in which case just the bot's username will be inserted.  **Note:** This offers an easy way for users to start using your bot in [inline mode](https://core.telegram.org/bots/inline) when they are currently in a private chat with it. Especially useful when combined with [*switch_pm…*](https://core.telegram.org/bots/api/#answerinlinequery) actions – in this case the user will be automatically returned to the  chat they switched from, skipping the chat selection screen. |
| switch_inline_query_current_chat | String                                                       | *Optional*. If set, pressing the button will insert the bot's username and the specified inline query in the current chat's input  field. Can be empty, in which case only the bot's username will be  inserted.  This offers a quick way for the user to open your bot  in inline mode in the same chat – good for selecting something from  multiple options. |
| callback_game                    | [CallbackGame](https://core.telegram.org/bots/api/#callbackgame) | *Optional*. Description of the game that will be launched when the user presses the button.  **NOTE:** This type of button **must** always be the first button in the first row. |
| pay                              | Boolean                                                      | *Optional*. Specify True, to send a [Pay button](https://core.telegram.org/bots/api/#payments).  **NOTE:** This type of button **must** always be the first button in the first row. |