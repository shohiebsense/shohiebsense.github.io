Not long ago since Kotlin `1.8.0` is released. This is quite big changes, one of them is to completely leave the Kotlin synthetic injection feature on xml.

Tried to update along with the app's dependencies. In my case its compose and bunch of those that related to it.

Some notes:
1. App's dependencies come first, so don't to do the other way around, you have to wait for the app's dependencies new version, test it then proceed to upgrade 
the kotlin. Then test it again if there are strange bugs.
2. Update manually instead improve the productivity. Relying on the IDE that lately has some issues will be a pain for you. If you are doing it manually 
you have total control about it.
3. Have a look at dependency manager tool at Tool Windows -> gradle.
4. You have to think upgrading package version is a critical, big thing, not trivial. 
