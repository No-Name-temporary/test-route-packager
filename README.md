# About
This respository contains the code the Test Route Packager lambda function, a component of the Seymour Active Monitoring Solution.

The Test Route Packager is the target for all scheduled EventBridge rules. Test Route Packager’s purpose is to read all the location data from the JSON test configuration payload delivered by an EB rule, and prep it for routing to [test runner](https://github.com/seymour-active-monitoring/test-runner) lambda functions in the the correct regions.

**Expected Shape of incoming test configuration JSON:**

```json
{
    "test": {
        "title": "my-first-test",
        "locations": [
            "us-east-1",
            "us-west-1",
        ],
        "minutesBetweenRuns": "60",
        "type": "api",
        "httpRequest": {
            "method": "post",
            "url": "https://myapi/api/users",
            "assertions": [
                {
                    "type": "responseTime",
                    "property": "",
                    "comparison": "lessThan",
                    "target": "500"
                }
            ]
        },
        "alertChannels": [
          {
            "type": "slack",
            "destination": "https://hooks.slack.com/services/...",
            "alertsOnRecovery": false,
            "alertsOnFailure": true
          }
        ]
    }
}
```

# Deployment

The Test Route Packager should be deployed along with the entire application. Refer to the following repo for detailed deployment instructions: [infra-setup](https://github.com/seymour-active-monitoring/infra-setup)