# MongoDB

- **Collection**: A bunch of documents. No schemas required.
- **Documents**: Basically JSON documents.

## Database Replication

- Duplicate database to handle more requests.
- By default MongoDB will create 1 primary database or 2 secondary databases.
- Write operations will be written to the primary and copied to the secondary.
