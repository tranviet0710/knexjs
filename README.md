
## Knex.js SQLite Example

This repository demonstrates a minimal Knex.js project using SQLite3. It includes a `knexfile.js`, a local `dev.sqlite3` database, and a `migrations/` folder with an example migration for a `cars` table.

### Contents

- `knexfile.js` — Knex configuration for the project.
- `dev.sqlite3` — SQLite database file (development).
- `migrations/` — Migration files. Example: `20250826110718_cars_table.js`.

### Prerequisites

- Node.js (recommended v14+)
- npm or yarn

### Install

Install dependencies:

```bash
npm install
# or
yarn install
```

### Configuration

The project uses the included `knexfile.js` which is already configured for the local `dev.sqlite3` file. If you need to change the database location or client, update `knexfile.js`.

### Migrations

Run migrations to create the database schema:

```bash
npx knex migrate:latest --knexfile knexfile.js
```

To rollback the last batch of migrations:

```bash
npx knex migrate:rollback --knexfile knexfile.js
```

The `migrations/20250826110718_cars_table.js` file defines a `cars` table; check it for the exact columns created.

### Quick usage (Node script)

You can interact with the database using Knex directly in a Node script. Example:

```js
const knex = require('knex')(require('./knexfile').development);

async function main() {
	const cars = await knex('cars').select('*');
	console.log(cars);
	await knex.destroy();
}

main().catch(err => { console.error(err); process.exit(1); });
```

Save that to a file (e.g., `list-cars.js`) and run `node list-cars.js`.

### Tests

No tests included by default. If you add tests, consider using an in-memory SQLite instance or a separate test database file and run migrations before the test suite.

### Development notes

- Keep migrations immutable once deployed to production; add new migrations for schema changes.
- Use `knex` CLI for migration and seed management.

### Useful commands

- Install dependencies: `npm install`
- Run migrations: `npx knex migrate:latest --knexfile knexfile.js`
- Rollback: `npx knex migrate:rollback --knexfile knexfile.js`

---

If you'd like, I can also add a small example script (e.g., `list-cars.js`) or a `package.json` script shortcuts to run migrations and queries. Tell me which you'd prefer.

