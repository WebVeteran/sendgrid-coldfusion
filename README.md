This library allows you to quickly and easily use the Twilio SendGrid Web API v3 via CFML.

# Table of Contents
* [Quick Start](#quick-start)

<a name="quick-start"></a>
# Quick Start

## Hello Email

The following is the minimum needed code to send an email:

```coldfusion
<!--- GENERATE YOUR PAYLOAD --->
<cfsavecontent variable="payload">
{
  "personalizations": [
    {
      "to": [
        {
          "email": "test@example.com",
          "name" : "Example User"
        }
      ]
    }
  ],
  "subject": "Sending with Twilio SendGrid is Fun",
  "content": [
    {
      "type" : "text/plain",
      "value": "and easy to do anywhere, even with Coldfusion"
    }
    {
      "type" : "text/html",
      "value": "and easy to do anywhere, even with <strong>Coldfusion</strong>"
    }
  ]
}
</cfsavecontent>

<!--- MAKE THE CALL --->
<cfhttp
  url="https://api.sendgrid.com/v3/mail/send"
  method="post"
  result="apicall">
  <cfhttpparam type="header" name="authorization" value="Bearer YOUR_SENDGRID_API_KEY">
  <cfhttpparam type="header" name="content-type" value="application/json">
  <cfhttpparam type="body" value="#payload#" />
</cfhttp>

<!--- WAS THERE AN ERROR? --->
<cfif apicall.statuscode does not contain '200'>
  <cfdump var="#deserializeJSON(apicall.fileContent)#">
</cfif>
```
