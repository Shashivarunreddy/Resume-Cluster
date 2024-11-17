
# Resume Clustering and Skill Search Application


This project is a web application for uploading, clustering, and searching resumes based on specific skills. It uses Flask for the backend, PostgreSQL for the database, and Bootstrap for styling. Users can upload CSV files of resumes for clustering or perform a skill-based search across resumes.


## Table of contents

 - [Features]()
 - [Tech Stack]()
 - [Installation]()
  - [Database Structure]()
 - [Usage]()


## Features

- Upload CSV files containing resumes.
- Cluster resumes based on textual similarity.
- Search resumes for specific skills.
- Visualize clustering results.

## Tech Stack

**Backend:** Flask

**Frontend:** HTML, CSS (Bootstrap)

**Database:** PostgreSQL

**Libraries:** Pandas, scikit-learn, Chart.js

## Installation
Prerequisites

1)Python (version 3.7 or higher)

2)PostgreSQL (version 12 or higher)

3)Git

### Steps to Set Up the Project

1. Clone the Repository

```bash
  git clone https://github.com/your-username/resume-clustering.git
  cd resume-clustering
```
2. Set Up Virtual Environment

```bash
  python3 -m venv venv
  source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

3. Install Requirements

```bash
  pip install -r requirements.txt
```
4. Configure PostgreSQL Database 

    Open PostgreSQL CLI or pgAdmin and create a new database and user.

```bash
CREATE DATABASE resume_db;
CREATE USER resume_user WITH PASSWORD 'your_password';
ALTER ROLE resume_user SET client_encoding TO 'utf8';
ALTER ROLE resume_user SET default_transaction_isolation TO 'read committed';
ALTER ROLE resume_user SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE resume_db TO resume_user;

```


 Update your database configuration in config.py (or .env file if used):

```bash
DATABASE_URI = 'postgresql://resume_user:your_password@localhost:5432/resume_db'

```

5. Initialize Database Tables

    Use the following structure to set up tables required for the project:

    Database Structure

```bash
CREATE TABLE resumes (
    id SERIAL PRIMARY KEY,
    filename VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    skills TEXT[]
);

CREATE TABLE clusters (
    id SERIAL PRIMARY KEY,
    cluster_id INT NOT NULL,
    resume_id INT REFERENCES resumes(id),
    summary TEXT
);

```


 Run the following commands to initialize the tables:

```bash
python manage.py db init
python manage.py db migrate
python manage.py db upgrade


```

6. Run the Application

   Start the Flask application by running:

```bash
flask run

```

The application will be available at http://127.0.0.1:5000.
## Usage/Examples

#### Uploading Resumes for Clustering

1)On the homepage, upload a CSV file containing resumes for clustering. 

2)The application will display the results on a new page with clusters and a bar chart.

#### Searching for Skills in Resumes

1)On the homepage, enter a skill to search for within resumes.

2) The search results page will display resumes that contain the specified skill.

