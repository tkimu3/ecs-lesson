## Create New Task Definition(restapi)

ECS - TaskDefinision - Create new Task Definision

type: FARGATE
Task definition name: ecs-sample-restapi
Network mode: awsvpc
OS: Linux
Task memory: 0.5
Task CPU: 0.25

"Add container"
    container name: sample-restapi
    image: 392618391476.dkr.ecr.us-west-1.amazonaws.com/ecs-sample-restapi:latest
    memory limits: Soft limit 128
    Port mapping: 8080
    ENVIRENMENT/CPUunits: 256

    "Add"

"Create task"

## Create New Service

ECS > Clusters > Cluster : ecs-lesson-cluster

"Create" button in "Service" tab
### Step 1: Configure service
    Launch type: FARGATE
    OS: Linux
    Task Definition: ecs-sample-restapi
    revision: 1(LATEST)
    cluster: ecs-lesson-cluster
    service name: ecs-sample-restapi
    Number of tasks: 2
    Minimum healthy percent: 100
    Maximum percent: 200

    "Next" button


### Step 2: Configure network

#### Configure network

#### VPC and security groups

    Cluster VPC: (ecs-lesson-vpc)
    Subnets: (Private subnet 1),(Private subnet 2)
    Security groups: "Edit" button
        "Select existing security group"
        - defalt (checked)
        - ecs_sg (checked)

        "Save"
    Auto-assign public IP: "DISABLED"

#### Load balancing
    None
    -> Because the containers can communicate within the ECS

#### Service disscovery
    (checked) Enable service discovery integration
    - Namespace : ecs.internal | PRIVATE
    - Service discovery name: sample-restapi



Step 3: Set Auto Scaling (optional)
Step 4: Review



