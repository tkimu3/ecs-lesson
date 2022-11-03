Service Discovery

```bash
aws servicediscovery create-service \
    --name sample-webapp \
    --dns-config 'NamespaceId="ns-4ehejbznsmmlfecl", DnsRecords=[{Type="A",TTL="60"}]' \
    --health-check-custom-config FailureThreshold=1 \
    --region us-west-1
```

````json
{
    "Service": {
        "Id": "srv-7ii3e2f3cbt4daky",
        "Arn": "arn:aws:servicediscovery:us-west-1:392618391476:service/srv-7ii3e2f3cbt4daky",
        "Name": "sample-webapp",
        "NamespaceId": "ns-4ehejbznsmmlfecl",
        "DnsConfig": {
            "NamespaceId": "ns-4ehejbznsmmlfecl",
            "RoutingPolicy": "MULTIVALUE",
            "DnsRecords": [
                {
                    "Type": "A",
                    "TTL": 60
                }
            ]
        },
        "Type": "DNS_HTTP",
        "HealthCheckCustomConfig": {
            "FailureThreshold": 1
        },
        "CreateDate": "2022-10-31T13:52:08.938000-07:00",
        "CreatorRequestId": "c9396076-9261-414c-9943-e50f9736f81b"
    }
}
```

Create ECS Service
```bash
aws ecs create-service \
    --cluster ecs-lesson-cluster \
    --service-name ecs-sample-webapp \
    --task-definition ecs-sample-webapp-task-def \
    --load-balancers '[{"targetGroupArn": "arn:aws:elasticloadbalancing:us-west-1:392618391476:targetgroup/ecs-sample-webapp/b244d7cb06c521f3", "containerName": "sample-webapp", "containerPort":8080 }, {"targetGroupArn":"arn:aws:elasticloadbalancing:us-west-1:392618391476:targetgroup/ecs-sample-webapp-8070/bddacaaff63c9f92","containerName": "sample-backend","containerPort":8070}]' \
    --desired-count 2\
    --platform-version LATEST \
    --launch-type FARGATE \
    --network-configuration '{"awsvpcConfiguration":{"subnets": ["subnet-0152c2e0444a36b83","subnet-087b1b58ce7d56c61"],"securityGroups":["sg-05e5a880103783c3e","sg-0aa0a774b8349435d"],"assignPublicIp":"DISABLED"}}' \
    --service-registries '[{"registryArn":"arn:aws:servicediscovery:us-west-1:392618391476:service/srv-7ii3e2f3cbt4daky"}]'
```

```
 ~/dev/ecs-lesson  main ?1  aws ecs create-service \                                                      ok  14:13:26
    --cluster ecs-lesson-cluster \
    --service-name ecs-sample-webapp \
    --task-definition ecs-sample-webapp-task-def \
    --load-balancers '[{"targetGroupArn": "arn:aws:elasticloadbalancing:us-west-1:392618391476:targetgroup/ecs-sample-webapp/b244d7cb06c521f3", "containerName": "sample-webapp", "containerPort":8080 }, {"targetGroupArn":"arn:aws:elasticloadbalancing:us-west-1:392618391476:targetgroup/ecs-sample-webapp-8070/bddacaaff63c9f92","containerName": "sample-backend","containerPort":8070}]' \
    --desired-count 2\
    --platform-version LATEST \
    --launch-type FARGATE \
    --network-configuration '{"awsvpcConfiguration":{"subnets": ["subnet-0152c2e0444a36b83","subnet-087b1b58ce7d56c61"],"securityGroups":["sg-0ad2f4d8e76a4cbf6","sg-0aa0a774b8349435d"],"assignPublicIp":"DISABLED"}}' \
    --service-registries '[{"registryArn":"arn:aws:servicediscovery:us-west-1:392618391476:service/srv-7ii3e2f3cbt4daky"}]'

```json
                "runningCount": 0,
                "failedTasks": 0,
                "createdAt": "2022-10-31T14:19:52.634000-07:00",
                "updatedAt": "2022-10-31T14:19:52.634000-07:00",
                "launchType": "FARGATE",
                "platformVersion": "1.4.0",
                "platformFamily": "Linux",
                "networkConfiguration": {
                    "awsvpcConfiguration": {
                        "subnets": [
                            "subnet-087b1b58ce7d56c61",
                            "subnet-0152c2e0444a36b83"
                        ],
                        "securityGroups": [
                            "sg-05e5a880103783c3e",
                            "sg-0aa0a774b8349435d"
                        ],
                        "assignPublicIp": "DISABLED"
                    }
                },
                "rolloutState": "IN_PROGRESS",
                "rolloutStateReason": "ECS deployment ecs-svc/2295447776932383817 in progress."
            }
        ],
        "roleArn": "arn:aws:iam::392618391476:role/aws-service-role/ecs.amazonaws.com/AWSServiceRoleForECS",
        "events": [],
        "createdAt": "2022-10-31T14:19:52.634000-07:00",
        "placementConstraints": [],
        "placementStrategy": [],
        "networkConfiguration": {
            "awsvpcConfiguration": {
                "subnets": [
                    "subnet-087b1b58ce7d56c61",
                    "subnet-0152c2e0444a36b83"
                ],
                "securityGroups": [
                    "sg-05e5a880103783c3e",
                    "sg-0aa0a774b8349435d"
                ],
                "assignPublicIp": "DISABLED"
            }
        },
        "healthCheckGracePeriodSeconds": 0,
        "schedulingStrategy": "REPLICA",
        "deploymentController": {
            "type": "ECS"
        },
        "createdBy": "arn:aws:iam::392618391476:root",
        "enableECSManagedTags": false,
        "propagateTags": "NONE",
        "enableExecuteCommand": false
    }
}
```
