## Requirements

To run the CLI you will need:

* Node.js (recommended: latest LTS version)
* npm or another Node package manager
* A configured environment file / config file -> See configuration chapter below
* Dependencies installed with `npm install`
* Postgresql DB

The project is written in TypeScript and the CLI entry point is `src/index.ts`.

---

## Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/choole/gator.git
cd gator
npm install
```

If the project uses TypeScript directly through Node, users may also need:

```bash
npm install -g ts-node typescript
```

---

## Configuration

Before running the CLI, create a configuration file.

Example:

```json
{
  "database_url": "postgres://user:password@localhost:5432/gator",
  "current_user_name": ""
}
```

Save it as:

```bash
~/.gatorconfig.json
```

or in the project root if the application expects a local config.

The config file is used to store:

* database connection information
* current logged-in user
* application state/settings

---

## Running the Program

You can run the CLI with:

```bash
npm start
```

or directly with TypeScript:

```bash
ts-node src/index.ts
```

Commands are passed through the CLI:

```bash
npm run start <command> [arguments]
```

---

## Example Commands

### Register a User

Creates a new user account.

```bash
npm run start register johndoe
```

---

### Login

Logs in as an existing user.

```bash
npm run start login johndoe
```

---

### Add a Feed

Adds a new RSS feed to the database.

```bash
npm run start addfeed "TechCrunch" https://techcrunch.com/feed/
```

---

### Follow a Feed

Follow an existing feed.

```bash
npm run start follow https://techcrunch.com/feed/
```

---

### List Feeds

Displays all feeds currently stored.

```bash
npm run start feeds
```

---

### Aggregate Posts

Starts the RSS aggregation loop.

Example with a 30 second interval:

```bash
npm run start agg 30s
```

---

### Browse Posts

Shows fetched posts from feeds.

```bash
npm run start browse
```

Limit results:

```bash
npm run start browse 10
```

---

## Typical Workflow

A common usage flow looks like this:

```bash
register johndoe
login johndoe
addfeed "Hacker News" https://news.ycombinator.com/rss
follow https://news.ycombinator.com/rss
agg 30s
browse
```

---

## Notes

* Make sure the database configured in the config file is running before starting the CLI.
* Commands regarding feeds and posts require a logged-in user.
* The aggregator command (`agg`) runs continuously until stopped manually.
