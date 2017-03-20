# Jmeter Performance Script

The test lives in the following repo: https://github.com/clearstorydata/performance
The code in the repo can be built via the following Jenkins job: http://jenkins.clearstorydata.com/view/Performance/job/performance.release/
The test can be run via the following Jenkins job: http://jenkins.clearstorydata.com/view/Performance/job/performance.run/

## Built Parameters

RampUp: This is the time in seconds of how long it will take to start all users/threads. I usually set RampUp = Users which means that each user/thread will start every second. In order to, for example, make the test more stressful on the system the RampUp time can be decreased making each thread start less than every second.

Loops: This parameter defines how many times each thread group is run. If, for example, 50 threads are configured to run 2 loops than all 50 threads must finish as part of the first loop in order for the second loop (second set of 50 threads starts) to start execution.

Storyboard_id: the storyboard ID is needed to validate the response times of summary page of that storyboard as well as the respnse times of the invididual tile calls. If storyboard id is left blank or the id does not eixst or is incorrect then related test steps will fail while the rest of the test steps will still pass.

Script: Currently there is only 1 script - e2e_data_steward_test.jmx. This script validates loging in as a data_steward and navigating to most of the pages of our app including Home Page, Data Sets List Page, DYML page, Groups page, Admin Page, Stories List page, Story page, Storyboards List page, Storyboard Summary page.

Story_id: the story id is needed to validate the response times of loading a given story. Similar to storyboard_id, if story_id is invalid/blank, the assocaited calls will result in invalid responses and failures while the rest of the script will execute normally

port: this is the web server port with default set to 443. The port can be updated depending on the port of the web server which is running the app to be tested

api_token: this parameter is needed specifically for the /render call which is used to validate the storyboard tile/frame retrievel response times. This token needs to belong to the user entered in the user_login parameter. If token is invalid/blank then the responses of the /render call and other tile retrievel calls will be invalid while the rest of the script will run normally.

## Understanding Results

Once the run is completed in Jenkins, follow below steps to understand the results:
1. Download .jtl file containing the results by clicking on "Last Successful Artifacts" and finding the appropriate .jtl file whose number matches the Jenkins build number of the test run. http://jenkins.clearstorydata.com/view/Performance/job/performance.run/lastSuccessfulBuild/artifact/results/
2. Open Jmeter and add a Summary Report from Listeners menu
3. Click on Browse and open the .jtl file downloaded in step 1
4. From this point, the summary report shows details of each and every test step aggregated by the number of threads. This report can then be exported in any format and further analysed with any tool.