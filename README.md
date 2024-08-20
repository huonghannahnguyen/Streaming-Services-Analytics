# Streaming-Services-Analytics

-- Dataset Link: https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies

-- Link Tableau Dashboard: https://public.tableau.com/app/profile/huong6399/viz/StreamingServicesAnalyticsDashboard/Story1

-- Netflix Table

--------- CREATE Netflix TABLE

    CREATE TABLE movies_netflix (id varchar, title varchar, type text,
	              description varchar, release_year int, age_certification varchar,
	              runtime int, genres varchar, production_countries varchar,
	              seasons decimal, imdb_id varchar, imdb_score decimal, imdb_votes decimal,
	              tmdb_popularity decimal, tmdb_score decimal);
 

    SELECT * FROM movies_netflix;    

--------- DATA CLEANING 
--------- Remove '' from genres and production countries

    UPDATE movies_netflix
    SET genres = REPLACE(REPLACE(REPlACE(genres, '[',''),']',''),'''','');

    UPDATE movies_netflix
    SET production_countries = REPLACE(REPLACE(REPLACE(production_countries,'[',''),']',''),'''','');
    
--------- Uppercase genres

    UPDATE movies_netflix
    SET genres = UPPER(genres);
    
--------- Add streaming_media column 

    ALTER TABLE movies_netflix
    ADD COLUMN streaming_media TEXT DEFAULT 'Netflix';

    SELECT * FROM movies_netflix;

![image](https://github.com/user-attachments/assets/becfa6a0-84da-4a68-9810-3d1cd2fabc0a)

-- HBO Max Table
---------- CREATE HBO Max TABLE 

    CREATE TABLE movies_HBOMax (id varchar, title varchar, type text,
	              description varchar, release_year int, age_certification varchar,
	              runtime int, genres varchar, production_countries varchar,
	              seasons decimal, imdb_id varchar, imdb_score decimal, imdb_votes decimal,
	              tmdb_popularity decimal, tmdb_score decimal);
 
--------- DATA CLEANING 
--------- Remove '' from genres and production countries

    UPDATE movies_HBOMax
    SET genres = REPLACE(REPLACE(REPlACE(genres, '[',''),']',''),'''','');

    UPDATE movies_HBOMax
    SET production_countries = REPLACE(REPLACE(REPLACE(production_countries,'[',''),']',''),'''','');
    
--------- Uppercase genres

    UPDATE movies_HBOMax
    SET genres = UPPER(genres);

--------- Add streaming_media column 

    ALTER TABLE movies_HBOMax
    ADD COLUMN streaming_media TEXT DEFAULT 'HBO Max';

    SELECT * FROM movies_HBOMax;

![image](https://github.com/user-attachments/assets/c48645f4-4f05-44c9-aadd-76aeabef66d7)
    
-- Hulu Table
-------- CREATE Hulu TABLE 

    CREATE TABLE movies_hulu (id varchar, title varchar, type text,
	              description varchar, release_year int, age_certification varchar,
	              runtime int, genres varchar, production_countries varchar,
	              seasons decimal, imdb_id varchar, imdb_score decimal, imdb_votes decimal,
	              tmdb_popularity decimal, tmdb_score decimal);
               
--------- DATA CLEANING
--------- Remove '' from genres and production countries

    UPDATE movies_hulu
    SET genres = REPLACE(REPLACE(REPlACE(genres, '[',''),']',''),'''','');

    UPDATE movies_hulu
    SET production_countries = REPLACE(REPLACE(REPLACE(production_countries,'[',''),']',''),'''','');
    
--------- Uppercase genres

    UPDATE movies_hulu
    SET genres = UPPER(genres);

--------- Add streaming_media column 

    ALTER TABLE movies_hulu
    ADD COLUMN streaming_media TEXT DEFAULT 'Hulu';

    SELECT * FROM movies_hulu;

![image](https://github.com/user-attachments/assets/82564d47-75e1-4f02-9412-e30534e74614)

-- Disney+ Table
---------- CREATE Disney+ TABLE

    CREATE TABLE movies_disney (id varchar, title varchar, type text,
	              description varchar, release_year int, age_certification varchar,
	              runtime int, genres varchar, production_countries varchar,
	              seasons decimal, imdb_id varchar, imdb_score decimal, imdb_votes decimal,
	              tmdb_popularity decimal, tmdb_score decimal);
 
--------- DATA CLEANING 
--------- Remove '' from genres and production countries

    UPDATE movies_disney
    SET genres = REPLACE(REPLACE(REPlACE(genres, '[',''),']',''),'''','');

    UPDATE movies_disney
    SET production_countries = REPLACE(REPLACE(REPLACE(production_countries,'[',''),']',''),'''','');

--------- Uppercase genres

    UPDATE movies_disney
    SET genres = UPPER(genres);

--------- Add streaming_media column 	

    ALTER TABLE movies_disney
    ADD COLUMN streaming_media TEXT DEFAULT 'Disney+';
	
    SELECT * FROM movies_disney;

![image](https://github.com/user-attachments/assets/2cec2e93-b3ee-4e87-bcbb-5f9fb4a3265f)

-- Amazon Prime Table
--------- CREATE Amazon Prime TABLE

    CREATE TABLE movies_amazon (id varchar, title varchar, type text,
	              description varchar, release_year int, age_certification varchar,
              	runtime int, genres varchar, production_countries varchar,
              	seasons decimal, imdb_id varchar, imdb_score decimal, imdb_votes decimal,
              	tmdb_popularity decimal, tmdb_score decimal);
               
--------- DATA CLEANING
--------- Remove '' from genres and production countries

    UPDATE movies_amazon
    SET genres = REPLACE(REPLACE(REPlACE(genres, '[',''),']',''),'''','');

    UPDATE movies_amazon
    SET production_countries = REPLACE(REPLACE(REPLACE(production_countries,'[',''),']',''),'''','');
    
--------- Uppercase genres

    UPDATE movies_amazon
    SET genres = UPPER(genres);

--------- Add streaming_media column 

    ALTER TABLE movies_amazon
    ADD COLUMN streaming_media TEXT DEFAULT 'Amazon Prime';
	
    SELECT * FROM movies_amazon;

![image](https://github.com/user-attachments/assets/c0010977-5fbe-4540-8da8-bbb7f10e3226)
    
-- Movies Table
--------- UNION ALL TABLES TOGETHER

    CREATE TABLE movies AS
    SELECT id, title, type, description, release_year, age_certification, runtime, genres,
	          production_countries, seasons, imdb_id, imdb_votes, tmdb_popularity, tmdb_score,
	          streaming_media FROM movies_netflix
    UNION 
    SELECT id, title, type, description, release_year, age_certification, runtime, genres,
	          production_countries, seasons, imdb_id, imdb_votes, tmdb_popularity, tmdb_score,
	          streaming_media FROM movies_hbomax
    UNION
    SELECT id, title, type, description, release_year, age_certification, runtime, genres,
          	production_countries, seasons, imdb_id, imdb_votes, tmdb_popularity, tmdb_score,
	          streaming_media FROM movies_amazon
    UNION
    SELECT id, title, type, description, release_year, age_certification, runtime, genres,
	          production_countries, seasons, imdb_id, imdb_votes, tmdb_popularity, tmdb_score,
	          streaming_media FROM movies_hulu
    UNION
    SELECT id, title, type, description, release_year, age_certification, runtime, genres,
	        production_countries, seasons, imdb_id, imdb_votes, tmdb_popularity, tmdb_score,
	        streaming_media FROM movies_disney;
         
-- Netflix Actors & Directors Table
--------- CREATE Netflix Actors & Directors TABLE

    CREATE TABLE cast_director_netflix (person_id int, id varchar, name text, character varchar,
	                role text);
                 
--------- Add streaming_media column 

    ALTER TABLE cast_director_netflix
    ADD COLUMN streaming_media text DEFAULT 'Netflix';

--------- CREATE HBO Max Actors & Directors TABLE

    CREATE TABLE cast_director_hbomax (person_id int, id varchar, name text, character varchar,
	                role text);
                 
--------- Add streaming_media column 

    ALTER TABLE cast_director_hbomax
    ADD COLUMN streaming_media text DEFAULT 'HBO Max';

-- Hulu Actors & Directors Table
--------- CREATE Hulu Actors & Directors TABLE

    CREATE TABLE cast_director_hulu (person_id int, id varchar, name text, character varchar,
	              role text);
 
--------- Add streaming_media column 

    ALTER TABLE cast_director_hulu
    ADD COLUMN streaming_media text DEFAULT 'Hulu';

-- Disney+ Actors & Directors Table
--------- CREATE Disney+ Actors & Directors TABLE

    CREATE TABLE cast_director_disney (person_id int, id varchar, name text, character varchar,
	              role text);
 
--------- Add streaming_media column 

    ALTER TABLE cast_director_disney
    ADD COLUMN streaming_media text DEFAULT 'Disney+';

-- Amazon Actors & Directors Table
--------- CREATE Amazon Actors & Directors TABLE

    CREATE TABLE cast_director_amazon (person_id int, id varchar, name text, character varchar,
	              role text);
 
--------- Add streaming_media column 	

    ALTER TABLE cast_director_amazon
    ADD COLUMN streaming_media text DEFAULT 'Amazon Prime';

-- Cast Director Table
--------- UNION ALL Actors & Directors TABLES TOGETHER

    CREATE TABLE cast_director AS
    SELECT person_id, id, name, character, role, streaming_media 
    FROM cast_director_amazon
    UNION 
    SELECT person_id, id, name, character, role, streaming_media 
    FROM cast_director_disney
    UNION
    SELECT person_id, id, name, character, role, streaming_media 
    FROM cast_director_hbomax
    UNION
    SELECT person_id, id, name, character, role, streaming_media 
    FROM cast_director_hulu
    UNION
    SELECT person_id, id, name, character, role, streaming_media 
    FROM cast_director_netflix;

-- Cast Director Movie Table
--------- JOIN movies AND cast_director TABLES TOGETHER

    CREATE TABLE cast_director_movie AS 
    SELECT cast_director.person_id, cast_director.id, cast_director.name, 
        	cast_director.character, cast_director.role, cast_director.streaming_media,
        	movies.title, movies.type, movies.release_year, movies.age_certification, 
        	movies.runtime, movies.genres, movies.seasons, movies.imdb_id,
        	movies.imdb_votes, movies.tmdb_popularity, movies.tmdb_score
    FROM cast_director
    FULL JOIN movies
    ON cast_director.id = movies.id AND cast_director.streaming_media = movies.streaming_media;
    
--------- ROUND NUMBERS AND REPLACE NULL WITH BLANK SPACE

    WITH first_table AS (SELECT id, title, type, COALESCE(description,'') AS description, release_year, COALESCE(age_certification,'') AS age_certification, 
                      	runtime, genres, production_countries, COALESCE(seasons::text,'') AS seasons, COALESCE(imdb_id::text,'') AS imdb_id, 
	                      ROUND(imdb_votes, 1) AS imdb_votes, ROUND(tmdb_popularity, 2) AS tmdb_popularity,
	                      ROUND(tmdb_score, 1) AS tmdb_score, streaming_media
                        FROM movies)

    SELECT id, title, type, description, release_year, age_certification, runtime, genres, production_countries,
	        seasons, imdb_id, COALESCE(imdb_votes::text,'') AS imdb_votes,
	        COALESCE(tmdb_popularity::text,'') AS tmdb_popularity, COALESCE(tmdb_score::text,'') AS tmdb_score, streaming_media
    FROM first_table;
    
-- Country Code Table
--------- CREATE country code TABLE

    CREATE TABLE country_code (country text, abbrev text)

--------- JOIN COUNTRY CODE TABLE WITH MOVIES TABLE AND SPLIT countries INTO DISTINCT countries 

    With split_country_table AS (
          SELECT TRIM(regexp_split_to_table(production_countries,',')) AS countries, streaming_media
          FROM movies), 
        
        count_country_table AS (SELECT DISTINCT countries, COUNT(countries), streaming_media
          FROM split_country_table
          GROUP BY countries, streaming_media),

        fix_table AS (SELECT CASE
          WHEN countries = 'United States of America' THEN 'US'
          WHEN countries = 'SUHH' THEN 'SU'
          ELSE countries
          END AS country, count AS movie_count, streaming_media
          FROM count_country_table)

        SELECT COALESCE(country_code.country,'') AS country, fix_table.country, 
                fix_table.movie_count, fix_table.streaming_media
        FROM fix_table
        LEFT JOIN country_code
        ON fix_table.country = country_code.abbrev
        
--------- SPLIT GENRES INTO INDIVIDUAL GENRE AND COUNT 

    WITH split_genres_table AS (
          SELECT TRIM(regexp_split_to_table(genres,',')) AS genres, streaming_media
          FROM movies)

        SELECT distinct genres, COUNT(genres), streaming_media
        FROM split_genres_table
        GROUP BY genres, streaming_media

![image](https://github.com/user-attachments/assets/3f29914a-c351-4a79-8149-65d7038279f6)
