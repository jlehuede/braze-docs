---
nav_title: Notify
article_title: Notify
description: "This reference article outlines the partnership between Braze and Notify, a real-time, omnichannel personalization solution that offers personalization across the customer lifecycle. Use Notify with Braze's Connected Content partner to easily drive marketing pressure and orchestrate in omnichannel"
alias: /partners/notify/
page_type: partner
search_tag: Partner
layout: dev_guide

---

<!-- In most cases, the ARTICLE_TITLE will be your company name. If your tool requires several seperate pages on Braze Docs, you can add a relevant page descriptor to your title, such as "MyCompany Analytics." -->
# Notify

<!-- The description starts with a '>' character and contains an introduction to your company, a link to your main site, and a consice overview of your integration. In a following paragraph, highlight the the relationship between your company and Braze and how this partnership helps your customers. -->
> 
Notify is an AI software, connected to CRM's tools, to help drive marketing pressure and orchestrate in omnichannel.
<br><br>
Giving access to exclusives futures such as : individualized perfect timing activation, sleepers awakeness, marketing pressure management, omnichannel orchestration (email, sms, push app, push web, wallet, whatsapp, ...) and carbon footprint reduction.
<br><br>
 We currently work in France and abroad (Europe + USA) with more than 100 brands from different sectors. 

<!-- Most partner integrations will require the following prerequisites. However, you may add additional prerequisites as needed. -->
## Prerequisites

Before you start, you'll need the following:

| Prerequisite          | Description                                                                                                                                |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
|  A Braze REST API key  | A Braze REST API key. <br><br> This can be created in the Braze dashboard from **Settings** > **API Keys**. |
| A Braze REST endpoint | [Your REST endpoint URL](https://rest.fra-01.braze.eu/campaigns/trigger/send). Your endpoint will depend on the Braze URL for your instance.                                                 |


<!-- Create step-by-step instructions for integrating your tool with Braze. It's important to be concise and only outline the minimum neccesary steps. -->
## Integrating Notify

### Step 1: Creation of a campaign
Customer created a campaign in Braze and share the campaign api_identifier with Notify

### Step 2: Creation of a segment 
Customer will create a segment in Braze and communicate the segmentId attached to the campaign. 

### Step 3: Fetch the segment
Notify will fetch with an API call the list of contacts in the segment attached to the campaign

Braze REST endpoint : `PARTNER_POST_URL`/users/export/segment

### Step 4: CNAME configuration
The CNAME allows the creation of Notify tracking links for opens and unsubscribes while maintaining the deliverability environment, ensuring that only the brand's domains are visible.

To create the CNAME, you need to access the DNS configuration file and add the following line to the zone file of mydomain.com:

### Step 5: Export of the database Opt-in                                              
**Exclusion:**  
Excludes any quarantines or blacklists.

**Fields:**

- Email
- Client ID
- Segment
- Sub-segment

**Details:**

- **Email:** A SHA256 hash of the email, converted to lowercase and with any leading or trailing spaces removed.
- **Segment:** The segment information defining the level of activity (active or inactive).
- **Sub-segment:** Any other relevant activity information (client/prospect, purchase activity level, RFM, etc.).

**Format:**

- Ideally a `.csv` file
- UTF-8 encoding
- Line breaks (`\n`)
- Semicolon (`;`) as the separator


### Step 6: Notify triggers the campaign 

Notify’s AI triggers the Braze campaign to send to a user at the time they deem to be most likely to engage

This is the curl request used by Notify to trigger sending of communications.

```bash
curl -X POST "PARTNER_POST_URL" \
-H "content-type: application/json" \
-d '{"braze_host":"BRAZE_API_ENDPOINT", \
"braze_api_key":"BRAZE_API_KEY", \
"PARTNER_host":"HOSTNAME", \
"PARTNER_token":"PARTNER_NAME_API_TOKEN"}'
```
                       


