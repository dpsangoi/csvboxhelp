---
description: 'Revision Date: 22 September 2022'
---

# User Data Policy

## Data Retention

Ensuring the privacy and security of user data is a top priority for us. You can rest easy, knowing that we take every precaution to provide an import service with high-grade security.

We provide a variety of data processing modes, including the [**Private Mode**](../destinations/private-mode.md). The following is the description of the Standard Mode.

When a user submits a file, CSVbox parses the file on the client side and then sends it to our servers. The data in transit is fully protected with a 256-bit SSL (Secure Socket Layer) connection that uses a SHA256 Certificate. This is the same level of protection used by online banking or e-commerce providers. &#x20;

We use databases from Amazon Web Services (AWS) with encryption enabled by default. The uploaded data is secured at rest and no one else can read it while it resides in our storage. Once the data is fully stored in our database, CSVbox then pushes it to your app or any other destination as configured by you in the dashboard.

<figure><img src="../.gitbook/assets/csvbox workflow.svg" alt=""><figcaption><p>Data flow in Standard Mode</p></figcaption></figure>

The user data from our storage is later deleted automatically after one month. Meanwhile, you can securely view and download this data anytime via the csvbox.io dashboard. We provide the option to get all the user-uploaded data deleted from our database (AWS S3) anytime with the click of a button. Lastly, you can configure the importer to completely bypass storing the data in our database (AWS S3).   &#x20;

The long-lived data about the import and the user files is not deleted. It mainly consists of supplementary log data helpful for troubleshooting and analyzing the import processes. This data does not include any original data from inside the user files.

## Data Residency

Data residency refers to where the data is stored in a geographical location. The location is important usually for regulatory or policy reasons. The data, uploaded by your users, goes through our servers and gets stored in our databases all located in the US by default.

We offer the option to configure the data residency location to US and Europe (Germany).

## Zero-knowledge design

csvbox.io collects, processes and stores only information that is required to run the service. We do not proactively build customer profiles, track metadata about the end-users or store unnecessary information in cookies unless our clients explicitly demand it to achieve their business goals.

With privacy at heart, we appreciate that the same business objectives can be achieved with multiple approaches. Processing unnecessary information represents a liability for us and risk for our clients, therefore by default, we prefer to design our features with a zero-knowledge approach.

If you have any specific questions you may raise a ticket [here](https://share.hsforms.com/1ubpg6RBoQgKOISkRMEViwg5auur).



## **GDPR** <a href="#gdpr" id="gdpr"></a>

* CSVbox.io is committed to users' right to data privacy and respects the spirit of the EU's General Data Protection Regulation.
* We now have a GDPR compliant [Data Processing Agreement (DPA)](gdpr/data-processing-addendum.md), that our customers can optionally sign with us.
* We're continuously working on adding more data control options (for activity log data and others).
* More information on our GDPR readiness is available [here](gdpr/).

{% hint style="info" %}
## User Data Policy Changelog

#### 06 April 2023

* Added text:

We provide a variety of data processing modes, including the [**Private Mode**](../destinations/private-mode.md). The following is the description of the Standard Mode.
{% endhint %}
