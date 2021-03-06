+++
title = "Introduction"
date = 2021-02-17T17:04:42-06:00
weight = 2
chapter = false
+++

In this workshop, you are going to learn about the **AWS Well-Architected Framework** focusing on a hands-on experience. The five labs in this Workshop are intended to guide you through the AWS Well-Architected pillars and help you understand how to improve an architecture using different strategies and AWS services.

These labs are designed *to be completed in sequence*, and the full set of instructions are documented below. Read and follow along to complete the labs. 

## The context

You work for an AWS Partner, and have a new customer, **AnyCompany**, which is a retail business. One of the main apps for the company is a product catalog; a web application that they recently migrated to the AWS Cloud from their on-premises environment. Even though the application is functional, the customer wants to have an architecture with best practices applied, because the business is growing. They are looking for an architecture that meets the new performance requirements, mitigates risks, and saves money. For them, it is crucial to use automation. 

The following is the initial architecture that you have found. Your mission is to improve upon it by applying some of the Well-Architected principles, according to the company’s needs.

<img src="images/starting.png" alt="drawing" width="600"/>

## Architecture review

You proposed doing a Well-Architected Framework Review (WAFR) of the customer’s environment to better understand the current status and their needs. After that review, you identified some insights, the most relevant of which are listed below:

1. They are performing a lot of operational tasks manually. The customer wants to automate the process to provide visibility into some important performance metrics, like memory or disk utilization. Additionally, they need a centralized log monitoring for DB and App. 

2.	It is clear for the customer that they need to have a highly available architecture.
3.	Security is their top priority. The more insights they can have available related to this topic, the better.
4.	They are not sure about the decision that they made when they chose a t2.micro instance to run the application. Performance is something that they do not want to sacrifice. AnyCompany people want to do some stress tests for the application, especially because they are expecting an increase in the demand on the application in the near future.
5.	Cost matters. The customer would like to have a clear visibility about costs and usage for the AWS Services. They would like to use a flexible tool for creating their own dashboards according to their needs. 

The information above is your starting point to help this customer enhance the architecture and achieve their objectives. You may identify more opportunities for improvement in this architecture but, for the purposes of the workshop, just focus on these findings.

## Target Architecture

After a Well-Architected Framework Review (WAFR), you and AnyCompany have defined a target architecture. This architecture will help the customer achieve their initial objectives. You are going to utilize the five Well-Architected pillars to implement the following architecture:

<img src="images/target-up.png" alt="drawing" width="1200"/>


## Labs:

This workshop is made up of five labs which align with each of the following five pillars of the [Well-Architected Framework](https://aws.amazon.com/well-architected):

-   [Operational Excellence](https://main.d2azidedm760yt.amplifyapp.com/work2/)
-   [Reliability](https://main.d2azidedm760yt.amplifyapp.com/work3/)
-   [Security](https://main.d2azidedm760yt.amplifyapp.com/work4/)
-   [Performance Efficiency](https://main.d2azidedm760yt.amplifyapp.com/work5/)
-   [Cost Optimization](https://main.d2azidedm760yt.amplifyapp.com/work6/)









	

