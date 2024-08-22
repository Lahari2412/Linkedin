# LinkedIn Research
---------------------------

## **Recruiter System Connect**

Recruiter System Connect synchronizes customers’ candidate information between your ATS and LinkedIn Recruiter. Once you have integrated with Recruiter System Connect, you may reach out to your Business Development Manager to discuss additional integrations such as Recommended Matches and Unified Search.

[Recruiter System Connect](https://learn.microsoft.com/en-us/linkedin/talent/recruiter-system-connect)

**Functionality of Recruiter System Connect**

- Rediscovered Candidates
- In-ATS Indicator
- One-Click Export
- Enhanced Profile Widget
- Retrieve InMail History
- Retrieve Note History
- Retrieve Stub Profiles after an InMail Response

1. **Development Prerequisites**
 
*Request Access*

Before developing with RSC, you need to develop an application with Job Posting first. Refer to [Job Posting API Overview](https://learn.microsoft.com/en-us/linkedin/talent/job-postings/api/sync-job-postings) to understand API Implementation details to create and manage jobs.

Next, you will need to be provisioned access to test resources, and your API applications will have to be enabled to access the Recruiter System Connect endpoints. You can request access by completing the following steps:

- [Create API applications](https://www.linkedin.com/developers/apps?appStatus=active) for the integration. You may create 2 API applications per integration - 1 for production, and 1 for development and testing.

- Please contact the member from LinkedIn Business Development who you have been working with and request to fill out the Partner Onboarding Form.
After the above steps, you'll be provided with various Test Credentials in the mail which you will consume for your development & testing. Next, ensure that:

* You can log into LinkedIn Recruiter
* You can access the One-Click Export and In-ATS indicator within LinkedIn Recruiter


If you are not yet a LinkedIn Talent Solutions Partner, please complete the [LinkedIn Talent Solutions Partner Request Form](https://business.linkedin.com/talent-solutions/ats-partners/partner-application)

2. **Begin Development**

*Get Started*

Once your application is configured, you may begin making API requests and testing the integration.

In order to implement Recruiter System Connect, LinkedIn has broken down the scope of integration into 5 Development Modules that can be found under [API & Plugin Guide](https://learn.microsoft.com/en-us/linkedin/talent/recruiter-system-connect/rsc-customer-configuration) documentation. As a customer or partner, you will need to utilize the components described within below modules:

[Module 1 - Configure Customer Applications and ATS Integrations](https://learn.microsoft.com/en-us/linkedin/talent/recruiter-system-connect/rsc-customer-configuration) : This module needs to be implemented by Partner ATS only. It describes the steps for customer onboarding for Partners.

[Module 2 - Sync Data from ATS to LinkedIn](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-jobs) : This module includes Middleware Platform APIs to sync candidates, applications, notes from ATS to LinkedIn. The data synced will show up in the ATS indicator in your Recruiter account.

[Module 3 - Retrieve Data from LinkedIn](https://learn.microsoft.com/en-us/linkedin/talent/recruiter-system-connect/retrieve-exported-candidates) : This module includes the Push Notification calls that LinkedIn makes to your callback URL to notify of One-Click Export & provide other updates. This also includes APIs to help you retrieve data from LinkedIn once you get these Push Notifications.

[Module 4 - Sync ACLs](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-acls) : This module includes APIs to help you define ACL permissions to control who all can access what data within your Recruiter account.

[Module 5 - Data Deletion](https://learn.microsoft.com/en-us/linkedin/talent/recruiter-system-connect/rsc-data-deletion) : This module includes all Entity Deletion APIs provided by LinkedIn's Middleware Platform.

3. **Development Tools**

We provide a snapshot of your integration journey in Project Planner Template. It provides a very helpful summary if you are just beginning development. We also provide few development tools like API Postman Collection, Sample Applications for testing Recruiter System Connect Plugins to assist in efficient, organized & speedy development. Refer to [Development Tools](https://learn.microsoft.com/en-us/linkedin/talent/recruiter-system-connect/rsc-development-tools) documentation for same.

4. **Required Fields**

We have put together required fields for all Recruiter System Connect APIs together at one place. Refer to Required Fields documentation to understand what all fields your ATS must provide.

5. **Certification**

Be sure to review the test cases per module required for your certification. These test cases should be demoed in your certification meetings. These are described in detail [here](https://learn.microsoft.com/en-us/linkedin/talent/recruiter-system-connect/rsc-certification).

## **Job Posting**

Before developing with RSC, you need to develop an application with Job Posting first. Refer to Job Posting API Overview to understand API Implementation details to create and manage jobs.

LinkedIn's Job Posting API enables authorized third parties such as clients, ATS systems, and job distributors to post jobs directly to LinkedIn on behalf of customers. This guide details on how to integrate with LinkedIn's Jobs Posting API.[Job Posting API](https://learn.microsoft.com/en-us/linkedin/talent/job-postings/api/overview)


[Associate Your LinkedIn Company ID with the LinkedIn Job Board](https://www.linkedin.com/help/linkedin/answer/a415420)



**Job Posting API Schema**

In order to publish a job, you need to construct the request body with all required fields. The more information your application can provide, the more candidates can be reached to satisfy customers’ needs. To post basic jobs, refer to [Foundation schema](https://learn.microsoft.com/en-us/linkedin/talent/job-postings/api/job-posting-api-schema#foundation-schema). To enable advanced features on job posting, refer to [Extension schema](https://learn.microsoft.com/en-us/linkedin/talent/job-postings/api/job-posting-api-schema#promoted-jobs-extension-schema)

**Post Jobs on LinkedIn**

*API Endpoint*

Use the following endpoint to submit a task to create, close, update, or renew one or more jobs asynchronously:

```http
POST https://api.linkedin.com/v2/simpleJobPostings
```

**API Authorization**

All requests below require access tokens obtained via the [OAuth2.0 Client Credentials flow](https://learn.microsoft.com/en-us/linkedin/shared/authentication/client-credentials-flow?tabs=HTTPS1).

>  *Important*
>
> We strongly recommend to use same access token for all concurrent and consecutive calls. An access token has a lifespan of 30 mins. Only on expiry of the existing token, new token should be generated.

### LinkedIn Sync Jobs

LinkedIn's Simple Job Posting API enables authorized third parties to post jobs directly to LinkedIn. This is an asynchronous API and you will receive a task id which you can use to see the status of the job, verify whether it successfully posted to LinkedIn, or see if there was an error during creation and view any details about the error.For further details view [LinkedIn Sync Jobs](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-jobs)

### LinkedIn Sync Candidates

All candidates should be sent via the Middleware Platform whenever they are created or updated in your ATS. Use your candidate identifier when syncing candidates via API.

To ensure the best possible ATS candidate to LinkedIn member match rate, sync phoneNumbers, linkedInProfileUrl, currentCompanyName, and currentJobTitle along with firstName, lastName, and emailAddresses whenever available

Use the following endpoint to create and update records:

```http
PUT https://api.linkedin.com/v2/atsCandidates?ids[0].atsCandidateId={id 1}&ids[0].dataProvider=ATS&ids[0].integrationContext={organization URN}&ids[1].atsCandidateId={id 2}&ids[1].dataProvider=ATS&ids[1].integrationContext={organization URN}
```

For each id specified in the request:

- Use your candidate id as the value of id[i].atsCandidateId .
- Use the customer's organization id as the value of id[i].integrationContext . The format should be "urn:li:organization:{id}".
- Use "ATS" as the value of id[i].dataProvider .

**Retrieve Candidate Matches**

After you've sent candidates to us, you may retrieve candidate details, which will include any algorithmic and user-supplied matches with LinkedIn members.

```https
GET https://api.linkedin.com/v2/atsCandidates?ids[0].atsCandidateId={id 1}&ids[0].dataProvider=ATS&ids[0].integrationContext={organization URN}&ids[1].atsCandidateId={id 2}&ids[1].dataProvider=ATS&ids[1].integrationContext={organization URN}&fields=matchedMembers,manualMatchedMember
```

For further details view [Sync Candidates](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-candidates)

## The Middleware Platform

The Middleware Platform represents a common set of APIs used to sync jobs, job applications, and talent profiles (such as candidates) between your ATS and LinkedIn on behalf of customers. Integrating with Middleware is essential for the Recruiter System Connect integration and powers a number of features.

**Getting Started**

All Middleware Platform operations are done on behalf of a customer. See Configure Customer Middleware Integrations for details on enabling and configuring customers to integrate with your ATS. This is a prerequisite.
If you're developing a Recruiter System Connect integration, check out the guide for important prerequisites before proceeding.


- **Sync Jobs**

  - When enabling a customer, use the Middleware Platform to send all historical jobs in bulk as a one-time process. Closed jobs must be included.
  - As jobs are created and updated by the customer, use the Middleware Platform to sync these new and updated jobs.

  - See [Sync Jobs](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-jobs) for technical details

- **Sync Candidates**

  - When enabling a customer, use the Middleware Platform to send all historical candidates in bulk as a one-time process. Then, retrieve and store the LinkedIn ID for each candidate.

  - As candidates are created, updated, and deleted by the customer, use the Middleware Platform to sync these new and updated candidates. Then, retrieve and store the LinkedIn ID for each candidate.

  -As candidates apply to jobs, link candidates with job applications

The Middleware Platform will automatically link the candidates you send with Recruiter profiles based on email address and other profile fields. If integrating with Recruiter System Connect, customers will also be able to link candidates manually using the Profile Plugin embedded in your ATS.

See [Sync Candidates](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-candidates) for technical details.

- **Sync Candidate Notes**

  - When enabling a customer, use the Middleware Platform to send all historical candidate notes in bulk as a one-time process.
  - As candidate notes are created and updated by the customer, use the Middleware Platform to sync these new and updated notes.
  See [Sync Candidates](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-candidate-notes) Notes for technical details.

- **Sync Job Applications**

  - When enabling a customer, use the Middleware Platform to send all historical job applications in bulk as a one-time process.

  - As job applications are submitted, updated, or deleted, use the Middleware Platform to sync these new and updated job applications.

  - As candidates apply to jobs, link candidates with job applications

  - Link new job applications with previously submitted job postings using your ATS's identifier.

See [Sync Job Applications](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-applications) for technical details.

- **Sync Job Application Notes & Interview Feedback**

  - When enabling a customer, use the Middleware Platform to send all historical job applications notes and interview feedback in bulk as a one-time process.

  - As job application notes and interview feedback are submitted and updated, use the Middleware Platform to sync these new and updated records.

 See [Sync Application Notes](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-application-notes) & [Interview Feedback](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-application-interview-feedback) for technical details. 

- **Sync Job Application Stages**

  - When enabling a customer, use the Middleware Platform to send the historical stages of a job application.

  - As job application changes its current stage, use the Middleware Platform to sync these new and updated records.

See [Sync Application Stages](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/sync-application-stages) for technical details.

- **Sync ACLs**

  - When enabling a customer, use the Middleware Platform to send all user-level entity security information in bulk as a one-time process.

  - As secured entities are created and updated by the customer, use the Middleware Platform to sync these new and updated entity/role associations.

  - As users are added to and removed from security groups or roles, use the Middleware Platform to sync these user/role associations.

See [ACL Overview](https://learn.microsoft.com/en-us/linkedin/talent/middleware-platform/acl-overview) for details.


## Recruiter Lite

- Find and hire talent

- Find great candidates, faster

- Contact top talent directly

- Build relationships with prospective hires


for further details [Perform API Linkedin search and export result](https://developer.unipile.com/docs/linkedin-search)

**How to Export Candidates From LinkedIn Recruiter**

LinkedIn Recruiter is a popular tool for companies using LinkedIn to recruit job candidates for open roles.

It provides recruiters with a massive database of professional profiles, advanced filters for laser-focused searches, candidate tracking capabilities, and in-platform messaging for communication and coordination.

But...

What if you wanted to take a list of candidates you've discovered using LinkedIn Recruiter, export it to a CSV or your ATS, and then reach out to each candidate by email or phone for better response rates than over LinkedIn?

You'll need to use a Chrome extension, like Wiza, to add export functionality to LinkedIn Recruiter and enrich candidates with verified personal email addresses and mobile numbers for outreach, which, is super easy.

In this step-by-step guide, I'll show you how to export candidates from LinkedIn Recruiter to a CSV or spreadsheet in 2024.

For complete overview [How to Export Candidates From LinkedIn Recruiter](https://www.linkedin.com/pulse/how-export-candidates-from-linkedin-recruiter-michael-kilcullen-omvce/)