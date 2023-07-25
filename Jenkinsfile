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
                def attachments = [
                     [
                        text: 'I find your lack of faith disturbing!',
                        fallback: 'Hey, Vader seems to be mad at you.',
                        color: '#ff0000'
                     ]
                ]
                slackSend(channel: "#jenkins", attachments: attachments)
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
