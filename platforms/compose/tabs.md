# Tabs



```kotlin

class TabsView: BaseViewCompose()
{
    @Composable
    override fun Root()
    {
        Tabs(viewKey)
    }
}

@Composable
fun Tabs(key: String)
{
    Surface {

        // create RouterTabs for this view
        val routerTabs = LocalRouter.currentOrThrow.createRouterTabs(key)

        Column(modifier = Modifier.fillMaxSize()) {

            // current page use routerTabs.tabIndex as the start value
            val page = remember { mutableIntStateOf(routerTabs.tabIndex) }

            // change pages only via routerTabs.route(0) don't change pages directly
            TabRow(selectedTabIndex = page.intValue) {
                Tab(selected = page.intValue == 0, onClick = { routerTabs.route(0) }) {
                    Text(text = "Tab 0")
                }
                Tab(selected = page.intValue == 1, onClick = { routerTabs.route(1) }) {
                    Text(text = "Tab 1")
                }
                Tab(selected = page.intValue == 2, onClick = { routerTabs.route(2) }) {
                    Text(text = "Tab 2")
                }
            }

            // user ComposeNavigatorTabs instead of ComposeNavigator
            ComposeNavigatorTabs(
                routerTabs = routerTabs,
                tabPaths = listOf(TabPath0(), TabPath1(), TabPath2()),
                selectedTab = page.intValue,
                onTabChanged = { page.intValue = it })
        }
    }
}
```

[Full example](https://github.com/AlexExiv/Router-Android/blob/main/sample-compose/src/main/java/com/speakerboxlite/router/samplecompose/tabs/TabsView.kt)
