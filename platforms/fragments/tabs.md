# Tabs

<figure><img src="../../.gitbook/assets/1.png" alt=""><figcaption></figcaption></figure>

```kotlin

class TabsFragment: FragmentViewModel<TabsViewModel>(R.layout.fragment_tabs),
    ViewTabs
{
    override fun onViewCreated(...)
    {
        super.onViewCreated(...)

        tabs.adapter = TabsAdapter(routerTabs, childFragmentManager, lifecycle)
        // Make offscreenPageLimit equals to number of pages
        tabs.offscreenPageLimit = TABS_MAP.size

        // Navigate to tab with index
        bottomNavigationView.setOnItemSelectedListener {
            routerTabs.route(TABS_MAP[it.itemId]!!)
        }

        // Add close tab stack to top behavior
        bottomNavigationView.setOnItemReselectedListener {
            routerTabs[TABS_MAP[it.itemId]!!].closeTabToTop()
        }

        // Give Router opportunity to change tabs
        routerTabs.tabChangeCallback = {
            bottomNavigationView.selectedItemId = TABS_BACK_MAP[it]!!
            tabs.setCurrentItem(it, false)
        }
    }

    companion object
    {
        val TABS_MAP = mutableMapOf(...) // tabId to tab's index
        val TABS_BACK_MAP = mutableMapOf(...) // tab's index to tabId
    }
}
```

```kotlin
class TabsAdapter(val router: RouterTabs, fm: FragmentManager, lifecycle: Lifecycle): 
            FragmentStateAdapter(fm, lifecycle)
{
    val hosterViews = mutableListOf<String>()

    init
    {
        for (i in 0 until itemCount)
        {
            val hv = when (i)
            {
                0 -> router.route(i, TabPath0(), false) // set root path for 0 tab
                1 -> router.route(i, TabPath1(), false) // set root path for 1 tab
                ...
                else -> TODO()
            }

            hosterViews.add(hv)
        }
    }

    // create HostFragment that contains RouterTab and hosts sub views
    override fun createFragment(position: Int): Fragment =
        HostFragment().also { it.viewKey = hosterViews[position] }

    override fun getItemCount(): Int = 5
}
```

[Full example](https://github.com/AlexExiv/Router-Android/tree/main/sample-fragment/src/main/java/com/speakerboxlite/router/sample/tabs)
