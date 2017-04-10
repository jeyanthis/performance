# Jmeter Performance Scripts Overview

The tests live in the following repo: https://github.com/clearstorydata/performance
The code in the repo can be built via the following Jenkins job: http://jenkins.clearstorydata.com/view/Performance/job/performance.release/
The tests can be run via the following Jenkins job: http://jenkins.clearstorydata.com/view/Performance/job/performance.run/

## 2 Scripts

e2e_data_steward_test.jmx: This script validates loging in as a data_steward and navigating to most of the pages of our app including Home Page, Data Sets List Page, DYML page, Groups page, Admin Page, Stories List page and Story page.
viewer_script.jmx: This script validates loging in as a viewer and navigating to Storyboards list page and Storyboard Summay page.

## Environment Details

Number of stories: 250
Number of datasets: 1800
Number of storyboards: 700
Number of users in organization: 120
Number of frames in storyboard: 10

## Built Parameters

RampUp: This is the time in seconds of how long it will take to start all users/threads. I usually set RampUp = Users which means that each user/thread will start every second. In order to, for example, make the test more stressful on the system the RampUp time can be decreased making each thread start less than every second.

Loops: This parameter defines how many times each thread group is run. If, for example, 50 threads are configured to run 2 loops than all 50 threads must finish as part of the first loop in order for the second loop (second set of 50 threads starts) to start execution.

Storyboard_id: the storyboard ID is needed to validate the response times of summary page of that storyboard as well as the respnse times of the invididual tile calls. If storyboard id is left blank or the id does not eixst or is incorrect then related test steps will fail while the rest of the test steps will still pass.

Script: Currently there are 2 scripts available - e2e_data_steward_test.jmx and viewer_script.jmx.which

Story_id: the story id is needed to validate the response times of loading a given story. Similar to storyboard_id, if story_id is invalid/blank, the assocaited calls will result in invalid responses and failures while the rest of the script will execute normally

port: this is the web server port with default set to 443. The port can be updated depending on the port of the web server which is running the app to be tested

api_token: this parameter is needed specifically for the /render call which is used to validate the storyboard tile/frame retrievel response times. This token needs to belong to the user entered in the user_login parameter. If token is invalid/blank then the responses of the /render call and other tile retrievel calls will be invalid while the rest of the script will run normally.

