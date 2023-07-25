import net.sf.json.JSONArray;
import net.sf.json.JSONObject;

pipeline {
    agent {
      kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        metadata:
          labels:
            some-label: some-label-value
        spec:
          containers:
          - name: python
            image: nctiggy/python-build-image
            command:
            - sleep
            args:
            - 99d
        '''
      }
    }

    environment {
        TEST_PREFIX = "test-IMAGE"
        TEST_IMAGE = "${env.TEST_PREFIX}:${env.BUILD_NUMBER}"
        TEST_CONTAINER = "${env.TEST_PREFIX}-${env.BUILD_NUMBER}"
        COVERALLS_TOKEN = credentials("coverallsToken")
    }

    stages {
        stage("something always do") {
            when {
                branch "main"
            }
            steps {
                script {
                blocks = [
	[
		"type": "section",
		"text": [
			"type": "mrkdwn",
			"text": "Hello, Assistant to the Regional Manager Dwight! *Michael Scott* wants to know where you'd like to take the Paper Company investors to dinner tonight.\n\n *Please select a restaurant:*"
		]
	],
    [
		"type": "divider"
	],
	[
		"type": "section",
		"text": [
			"type": "mrkdwn",
			"text": "*Farmhouse Thai Cuisine*\n:star::star::star::star: 1528 reviews\n They do have some vegan options, like the roti and curry, plus they have a ton of salad stuff and noodles can be ordered without meat!! They have something for everyone here"
		],
		"accessory": [
			"type": "image",
			"image_url": "https://s3-media3.fl.yelpcdn.com/bphoto/c7ed05m9lC2EmA3Aruue7A/o.jpg",
			"alt_text": "alt text for image"
		]
	]
]
                }
                slackSend(channel: "#jenkins", blocks: blocks)
            }
        }
        stage("something on tag") {
            when {
                buildingTag()
            }
            steps {
                slackSend color: "good", message: "Message from Jenkins Tag"
            }
        }
    }
}
