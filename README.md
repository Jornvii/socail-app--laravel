




.... Feature of app
------ authentication ( login , registration , logout)
------ user profile ( update ,delete)
------ post ( create, update, delelte, like comment)

database schema :

*user
-id  begint primary key auto-increment
-name varchar(50) not null, 
-email varchar(50) not null, unique   (email can'nt be same)
-password varchar(50) not null
-profile_pic varchar(50)
-bio text nullable