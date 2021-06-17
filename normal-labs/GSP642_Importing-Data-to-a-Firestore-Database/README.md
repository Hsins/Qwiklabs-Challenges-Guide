# GSP642 —— Importing Data to a Firestore Database

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><em>（🔎 Click to expand／collapse）</em></small>
  </summary>

- [Overview](#overview)
- [Architecture](#architecture)
- [Setup Firestore in Google Cloud](#setup-firestore-in-google-cloud)
- [Example Code: Database Importing](#example-code-database-importing)
- [Add Developer to the Project without Giving Firestore Access](#add-developer-to-the-project-without-giving-firestore-access)
- [References](#references)

</details>

## Overview

For the labs in the [Google Cloud Serverless Workshop](https://google.qwiklabs.com/quests/98): Pet Theory Quest, you will read through a fictitious business scenario and assist the characters with their serverless migration plan.

Twelve years ago, Lily started the Pet Theory chain of veterinary clinics. The Pet Theory chain has expanded rapidly over the last few years. However, their old appointment scheduling system is not able to handle the increased load, so Lily is asking you to build a cloud-based system that scales better than the legacy solution.

Pet Theory's Ops team is a single person, Patrick, so they need a solution that doesn't require lots of ongoing maintenance. The team has decided to go with serverless technology.

Ruby has been hired as a consultant to help Pet Theory make the transition to serverless. After comparing serverless database options, the team decides to go with [Cloud Firestore](https://firebase.google.com/docs/firestore). Since Firestore is serverless, capacity doesn't have to be provisioned ahead of time which means that there is no risk of running into storage or operations limits. Firestore keeps your data in sync across client apps through real-time listeners and offers offline support for mobile and web, so a responsive app can be built that works regardless of network latency or Internet connectivity.

## Architecture

This diagram gives you an overview of the services you will be using and how they connect to one another:

<div align="center">
  <img src="https://i.imgur.com/BQI74BU.png" alt="Architecture">
</div>

## Setup Firestore in Google Cloud

1. Click **Navigation Menu** > **Firestore**.
2. Click **SELECT NATIVE MODE** or **SELECT DATASTORE MODE** button.
    - **Native Mode**: good for letting lots of users access the same data at the same time and it has features like real-time updates and direct connection between your database and web/mobile clients.
    - **Datastore Mode**: puts an emphasis on high throughput (lots of reads and writes).
3. Click **CREATE DATABASE**.

## Example Code: Database Importing

```javascript
const { Firestore } = require('@google-cloud/firestore');

const db = new Firestore();

function writeToFirestore(records) {
  const batchCommits = [];
  let batch = db.batch();
  records.forEach((record, i) => {
    let docRef = db.collection('customers').doc(record.email);
    batch.set(docRef, record);
    if ((i + 1) % 500 === 0) {
      console.log(`Writing record ${i + 1}`);
      batchCommits.push(batch.commit());
      batch = db.batch();
    }
  });
  batchCommits.push(batch.commit());
  return Promise.all(batchCommits);
}

async function importCsv(csvFileName) {
  const fileContents = await readFile(csvFileName, 'utf8');
  const records = await parse(fileContents, { columns: true });
  try {
    await writeToFirestore(records);
  }
  catch (e) {
    console.error(e);
    process.exit(1);
  }
  console.log(`Wrote ${records.length} records`);
}
```

## Add Developer to the Project without Giving Firestore Access

We can ensure the developers should only be able to read the system logs and not be able to read or modify the data in Firestore.

- `roles/source.viewer`: lets members read the logs
- `roles/source.writer`: lets members read and write the source control repository

```bash
# add roles to the developer
$ gcloud projects add-iam-policy-binding <PROJECT_ID> \
    --member="user:<EMAIL>"user:[EMAIL] \
    --role="<ROLE>"
```

## References

- [Firestore Documentation](https://cloud.google.com/firestore/docs)
- [rosera/pet-theory | GitHub](https://github.com/rosera/pet-theory)
- [Understanding roles | Cloud Identity and Access Management Documentation](https://cloud.google.com/iam/docs/understanding-roles#predefined_roles)