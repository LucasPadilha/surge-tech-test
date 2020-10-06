# Surge Tech Test

### Content

The `markdown` directory has the original markdown files.

The `html` directory has the HTML converted files.

The `diagrams` directory has the `Class Diagram`, which has an abstract first version of the core classes needed to build the API.

### API design

I've opted to go with a REST API, using a combination of `Access` and `Refresh` tokens to authenticate and authorize `Users` and `Customers` accesses.

### Email marketing solution

My take on the bulk email sending feature works with a combination of internal API, third-party (Sendgrid) API, queueing campaigns and running the script on the background, using `CRON` jobs to avoid application blocking.

In order to use this solution, the client must create the dynamic templates using Sendgrid, then queue the campaign using the API and provide the Sendgrid template ID, then the `CRON` script uses the given template and replaces all data placeholders with `Customers` details.
