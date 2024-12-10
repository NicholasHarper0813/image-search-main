## Setup
### Creating a KV Database Instance

### Creating a Postgres Database Instance

### Creating a Blob Instance

## Running locally

> Note: You should not commit your `.env` file or it will expose secrets that will allow others to control access to your various OpenAI and authentication provider accounts.

1. Install Vercel CLI: `npm i -g vercel`
2. Link local instance with Vercel and GitHub accounts (creates `.vercel` directory): `vercel link`
3. Download your environment variables: `vercel env pull`

```bash
pnpm install
```

## Add OpenAI API Key
Be sure to add your OpenAI API Key to your `.env`.

## Database Setup
To push your schema changes to your Vercel Postgres database, run the following command.
```bash
pnpm run db:generate
pnpm run db:push
```

## Prepare your Images (Indexing Step)
To get your application ready for Semantic search, you will have to complete three steps.
1. Upload Images to storage
2. Send Images to a Large Language Model to generate metadata (title, description)
3. Iterate over each image, embed the metadata, and then save to the database

### Upload Images
Put the images you want to upload in the `images-to-index` directory (.jpg format) at the root of your application. Run the following command.
```bash
pnpm run upload
```
This script will upload the images to your Vercel Blob store.
Depending on how many photos you are uploading, this step could take a while.

### Generate Metadata
Run the following command.
```bash
pnpm run generate-metadata
```
This script will generate metadata for each of the images you uploaded in the previous step.
Depending on how many photos you are uploading, this step could take a while.

### Embed Metadata and Save to Database
Run the following command.
```bash
pnpm run embed-and-save
```
Depending on how many photos you are uploading, this step could take a while. This script will embed the descriptions generated in the previous step and save them to your Vercel Postgres instance.

## Starting the Server
Run the following command
```bash
pnpm run dev
```
Your app template should now be running on [localhost:3000](http://localhost:3000/).

## Authors
Nicholas Harper
