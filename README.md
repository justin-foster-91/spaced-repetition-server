# Spaced repetition API!

## Japanese Spaced Repetition Server
This repo creates the server side API for the Japanese Language - Spaced Repetition App (a mouthful). 

There is no need to clone or run code locally. 

You can go to the live [Japanese Language SR](https://spaced-repetition-xi.vercel.app) app directly to use. 
You can visit the [Japanese Language SR app repo](https://github.com/thinkful-ei-quail/SR-Client-Sonali-Justin) to view the front end code. 

**created by:** Sonali Najera and Justin Foster

## Summary

The API connects client and server for the Japanese Language SR application. The API allows for CRUD operations listed below to be accessed at specific endpoints to:
 

 - Create new: 
	 - Users
	 - User scores
	
 - Retrive: 
	 - User information
	 - Languages available
	 - Words available
	 - Correct/Incorrect scores
- Update:
	- User scores
	- Next words in line
	 
## Technology Stack
This server was created using Node.js, Express.js and Postgresql.

## Endpoints (How to use)

### Open Endpoints

#### 1. Create User

Used to create a new account for a User.

**URL**  `/api/users/`

**METHOD**  `POST`

**Auth Required**  `No`

##### Constraints

Must include the following fields in original request

    {
      "username": "someUsername",
      "password": "someP@ssword1",
      "name": "someName",
    }

####  Success Response

**Code**:  `201 ok`

**Content**

    {
     id:  user.id,
	 name:  user.name,
	 username:  user.username,
    }

#### Error Response

**Condition 1**: Missing a required field in request body

**Code**  :  `400 BAD REQUEST`

**Content**  :

    {
      "error": "Missing [SPECIFIC FIELD] in request body"
    }

**Condition 2**: Username already exists. 

**Code** : `400 BAD REQUEST`

**Content** : 
``` json
{
  "error": "Username already taken"
}
```

#### 2.  User Login

Used to sign in a User.

**URL**  `/api/auth/token`

**METHOD**  `POST`

**Auth Required**  `No`

##### Constraints

Must include the following fields in original request

    {
      "username": "someUsername",
      "password": "someP@ssword1"
    }

### Protected Endpoints

#### 3. Get Words

Used to retrieve Words available in database.

**URL**  `/api/language/`

**METHOD**  `Get`

##### Constraints

Must include the following fields in original request

    headers:{
      'authorization': `bearer SOME TOKEN`
    }
    
#### 4. Get Head

Used to retrieve the head which points to the next word in list.

**URL**  `/api/language/head`

**METHOD**  `Get`

##### Constraints

Must include the following fields in original request

    headers:{
      'authorization': `bearer SOME TOKEN`
    }
    
 #### 5. Post Guess

Used to post user guess and check against database 

**URL**  `/api/language/guess`

**METHOD**  `POST`

##### Constraints

Must include the following fields in original request

    body:{
      'guess': `user input`
    }

## Contact
Feel free to reach out if you notice bugs or have questions about the code. 

> Written with [StackEdit](https://stackedit.io/).

## Local dev setup

If using user `dunder-mifflin`:

```bash
mv example.env .env
createdb -U dunder-mifflin spaced-repetition
createdb -U dunder-mifflin spaced-repetition-test
```

If your `dunder-mifflin` user has a password be sure to set it in `.env` for all appropriate fields. Or if using a different user, update appropriately.

```bash
npm install
npm run migrate
env MIGRATION_DB_NAME=spaced-repetition-test npm run migrate
```

And `npm test` should work at this point

## Configuring Postgres

For tests involving time to run properly, configure your Postgres database to run in the UTC timezone.

1. Locate the `postgresql.conf` file for your Postgres installation.
   1. E.g. for an OS X, Homebrew install: `/usr/local/var/postgres/postgresql.conf`
   2. E.g. on Windows, _maybe_: `C:\Program Files\PostgreSQL\11.2\data\postgresql.conf`
   3. E.g  on Ubuntu 18.04 probably: '/etc/postgresql/10/main/postgresql.conf'
2. Find the `timezone` line and set it to `UTC`:

```conf
# - Locale and Formatting -

datestyle = 'iso, mdy'
#intervalstyle = 'postgres'
timezone = 'UTC'
#timezone_abbreviations = 'Default'     # Select the set of available time zone
```

## Scripts

Start the application `npm start`

Start nodemon for the application `npm run dev`

Run the tests mode `npm test`

Run the migrations up `npm run migrate`

Run the migrations down `npm run migrate -- 0`
