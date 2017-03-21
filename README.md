# droid-tests

Current Android UI Tests.

•	Tests continue to fail with timeouts, when more than 1 device is sent at once
•	Each test step, carries an application startup time lasting 1:20, on average (1 min + 20 sec), before any test steps are executed. This leaves, at minimum, 90 minutes for runtime of the current 90 tests set to run for Category “MustTest” – this should be looked into further, it seems it can be reduced.

Folder structure --------------------------------------------------------------------

apk_packages_test
    --> holds last used .apk files, submitted for tests

archives
    --> zipped archives of device test runs

Asus Google Nexus 7 - Android 4.4.4 (device param id = --devices 28ac0ab1)
    --> holds test-run diagnosis logs for this device, 4.4.4 API only

Motorola Nexus 6 - Android 5.1 (device param id = --devices d75aaa8a)
    --> holds test-run diagnosis logs for this device, 5.1 API only

Huawei Nexus 6P - Android 6.0.1 (device param id = --devices 4be46a6d)
    --> holds test-run diagnosis logs for this device, 6.0.1 API only

LG Nexus 5X - Android 7.0 (device param id = --devices d9270006)
    --> holds test-run diagnosis logs for this device, 7.0 API only

notes
    --> gathered notes, text, scratch-pads used throughout testing and changes

------------------------------------------------------------------------------------

Changes made
abstract class FeatureTestBase:
•	Addition of querying if common element exists, prior to it being waited on. Elements affected: ”agreeAndContinueButton” and ”skipButton”.


[Category("AboutUsTests")] 
•	example of change, removal of spaces for category, for each test class

[Category("Set01")] 
•	an intermediary category created when resolving successful tests from those needing more review (commented-out [test], in that case)

Continuously failing tests commented out:
•	//[Test]
//TODO: failed - System.Exception : Error while performing WaitForElement(Marked("Job 1"), "Timed out waiting for element...", null, null, null) ----> System.TimeoutException : Timed out waiting for element... 



Possible Remaining Modifications
1.	Reduce the application startup time, or resolve the UI-Test initial start-up being required for each test step currently.
2.	Update TeamCity to reflect the modifications on the test-cloud params (see test-cloud typical params used below).
3.	Possibly review the APISetup action, and utilize a Mock authentication, or group tests with a single authentication for those “Musttest” critical UI-test runs. 


Test-Cloud cmd-line params used:

mono CareerBuilder-Search/packages/Xamarin.UITest.1.3.15/tools/test-cloud.exe submit /Users/dev/apk_packages/com.careerbuilder.SugarDrone.apk 5ea65885581eb92616d2130d9ff8b78c --devices 4be46a6d --series "test" --locale "en_US" --app-name "Job Search Cats" --user consumermobileapps@careerbuilder.com --assembly-dir CareerBuilder-Search/CareerBuilder_Search.DroidFeatureTests/bin/Debug/ --async --include AppStartTests --include MustTest --test-param screencapture:true,debug:true --test-chunk



