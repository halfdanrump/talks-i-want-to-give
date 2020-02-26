# From Classic Cron to Serverless Task Management (with Python)

# Elevator Pitch
If you run scripts for batch processing and use cron a lot, you should listen to this talk. I will show you how SnapDish uses Airflow to execute Python scripts in the serverless ECS Fargate platform. You will see that getting started with distributed task scheduling is much easier than you thought.


## Overview
This is a "here's what I did and what I learned"-type of talk, in which I want to show you that it's fairly straightforward to change from simple cron scheduling on a single VM to distributed task execution on the serverless Fargate platform and scheduling handled by Apache Airflow. I will give a brief overview of each of these technologies, explain the pros/cons of each and why I decided to use them. At the end I will give you a simple recipe to follow so that you can emulate my setup if you wish.

## The Starting Point: Cron On a Single VM
At SnapDish we run a lot of batch processing jobs for recommendation systems, AI tasks, BI intelligence and more. For many years we were  running all our batch script on a single beefy VM. Overall it worked pretty well. However, as the number of scripts grew the load on the server became more unpredictable.nA new risk was introduced; if several memory intensive scripts were to be executed at the same time, the entire server might crash.

## Moving to ECS Fargate
As a solution to this, I migrated some of the resource intensive scripts to AWS ECS Fargate.

### What is Fargate
ECS Fargate is essentially serverless Docker, in that it lets you run Docker containers without having to manage a Docker host yourself. Since you don't have to worry about the underlying infrastructure, the only limit to how many containers you want to run is the limit on your credit card. Fargate makes it easy to overcome to problem of jobs fatally competing for resources. I migrated some of our heavy tasks to Fargate, and everything was good for a while.

### Fargate Limitations
Unfortunately it quickly turned out that Fargate left much to be desired when it came to task monitoring. "The task failed, but when, and why?" - was a common question that I found myself having to answer often. The way that Fargate is designed often made finding the answer a painstaking process. Another serious limitation of Fargate is that the functionality for scheduling tasks is identical to cron. In a nutshell, Fargate cannot model complex workflows where one script depends on the results of another script.

Once I realized the limitations of Fargate, I started looking for another tool. And finally, I found Airflow.


## Arriving at Airflow
There are a lot of different tools out there for managing workflows. A big reason for why I ended up selecting Airflow was that it could do everything I needed, excellent documentation and a good community for support. Airflow was compatible with my requirements for the following reasons: First of all,  **tasks can be anything executable.** In my case, I wanted to run Docker containers running in ECS Fargate. Next, **Airflow can handle Jobs with workflows**, which means that Airflow handles task dependencies by modeling all jobs as Directed Acyclic Graphs (DAGs). **DAGs are written in Python**, which allowed me to call AWS resources with `boto3`, and write re-usable library code. Finally Airflow comes packed with **great monitoring of task status and execution history**.

### Is Airflow Difficult?

Airflow has a reputation of being difficult to use. While I don't think it's as bad as people think, I did run into some very frustrating issues that I will tell you about so that you won't have to deal with them.

## Closing With a Demo
Finally, I'll round off with a demo. I will show you Airflow in action by creating a simple DAG, execute it in Fargate and view the logs in the Airflow dashboard.
