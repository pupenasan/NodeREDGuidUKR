# SidebarFunction



![image-20230517125454658](media/image-20230517125454658.png)

## sidebarAccordion

Default data

```
{{main.user.auth_module.user.menu}}
```

Default Selected Item

```
{{main.URL.queryParams.pageName}}
```

onClickMain

```
{ { navigateTo(sidebarAccordion.category, {
	pageName: sidebarAccordion.category
}) } }
```

onClick

```
{ { navigateTo(sidebarAccordion.categoryItem, {
	pageName: sidebarAccordion.categoryItem
}) } }
```

onClickSub

```
{ { navigateTo(sidebarAccordion.categorySubItem, {}) } }
```

