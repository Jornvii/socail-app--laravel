1. User Table:
id: Primary key, unique identifier for each user.
name: The user’s display name (maximum of 50 characters).
email: User’s unique email address, used for login.
hashed_password: Securely stored password after being hashed (bcrypt or similar).
profile_pic: URL or file path for the user’s profile picture (nullable).
bio: Short bio or description for the user (optional).
created_at: Timestamp when the user was created, for record-keeping.
updated_at: Automatically updated whenever the user profile changes.
deleted_at: Used for soft deletion; when set, it marks the user as deleted without permanently removing them from the database.

2. Post Table:
id: Primary key, unique identifier for each post.
user_id: Foreign key to the User table, indicating the post's author.
caption: The content or text of the post.
image_url: URL or file path to an image associated with the post (nullable).
is_published: Boolean flag to indicate if the post is published or saved as a draft.
created_at: Timestamp when the post was created.
updated_at: Automatically updated when the post is modified.
deleted_at: Used for soft deletion of posts.
Foreign Key (user_id): Ensures posts are linked to a valid user and deletes posts if the user is deleted (on cascade).

3. Like Table:
id: Primary key, unique identifier for each like.
user_id: Foreign key to the User table, identifying who liked the post.
post_id: Foreign key to the Post table, identifying the post that was liked.
created_at: Timestamp indicating when the like was created.
Foreign Key (user_id): Links the like to the user who performed the action.
Foreign Key (post_id): Links the like to the post.
UNIQUE (user_id, post_id): Ensures that a user can like a post only once.

4. Comment Table:
id: Primary key, unique identifier for each comment.
user_id: Foreign key to the User table, identifying the user who made the comment.
post_id: Foreign key to the Post table, identifying the post being commented on.
text: The content of the comment.
created_at: Timestamp indicating when the comment was created.
Foreign Key (user_id): Ensures comments are linked to valid users and can cascade deletes (delete comments when the user is deleted).
Foreign Key (post_id): Ensures comments are linked to valid posts.

5. Follow Table (Optional):
id: Primary key, unique identifier for each follow record.
follower_id: Foreign key to the User table, indicating the user who is following someone.
following_id: Foreign key to the User table, indicating the user who is being followed.
created_at: Timestamp when the follow action occurred.
Foreign Key (follower_id): Links the follower to the User table.
Foreign Key (following_id): Links the followed user to the User table.
UNIQUE (follower_id, following_id): Prevents a user from following the same person multiple times.

6. Notification Table:
id: Primary key, unique identifier for each notification.
user_id: Foreign key to the User table, identifying the recipient of the notification.
post_id: Foreign key to the Post table, identifying the post that triggered the notification.
type: Enum value representing the type of notification (e.g., 'like' or 'comment').
read: Boolean indicating whether the user has read the notification.
created_at: Timestamp indicating when the notification was created.
Foreign Key (user_id): Links the notification to the user receiving it.
Foreign Key (post_id): Links the notification to the relevant post.


-******************************************** Laravel Passport
https://laravel.com/docs/10.x/passport

🌞 composer require laravel/passport
🔥 if can't in satall ---> composer require laravel/passport --ignore-platform-req=ext-sodium
🌞php artisan migrate
🌞

-******************************************** Laravel Passport
https://laravel.com/docs/10.x/passport

🌞 composer require laravel/passport
🌞
🌞
🌞

-******************************************** Laravel Passport
https://laravel.com/docs/10.x/passport

🌞 composer require laravel/passport
🌞
🌞
🌞

-******************************************** Laravel Passport
https://laravel.com/docs/10.x/passport

🌞 composer require laravel/passport
🌞
🌞
🌞















****************************************************************
Data create
-- User Table
CREATE TABLE User (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(50) NOT NULL UNIQUE,
    hashed_password VARCHAR(255) NOT NULL,
    profile_pic VARCHAR(255) DEFAULT NULL,
    bio TEXT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP NULL
);


-- Post Table
CREATE TABLE Post (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT,
    caption TEXT NOT NULL,
    image_url VARCHAR(255) DEFAULT NULL,
    is_published BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP NULL,
    FOREIGN KEY (user_id) REFERENCES User(id) ON DELETE CASCADE
);


-- Like Table
CREATE TABLE Like (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT,
    post_id BIGINT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES User(id) ON DELETE CASCADE,
    FOREIGN KEY (post_id) REFERENCES Post(id) ON DELETE CASCADE,
    UNIQUE (user_id, post_id)
);


-- Comment Table
CREATE TABLE Comment (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT,
    post_id BIGINT,
    text TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES User(id) ON DELETE CASCADE,
    FOREIGN KEY (post_id) REFERENCES Post(id) ON DELETE CASCADE
);


-- Follow Table (Optional)
CREATE TABLE Follow (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    follower_id BIGINT,
    following_id BIGINT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (follower_id) REFERENCES User(id) ON DELETE CASCADE,
    FOREIGN KEY (following_id) REFERENCES User(id) ON DELETE CASCADE,
    UNIQUE (follower_id, following_id)
);


-- Notification Table
CREATE TABLE Notification (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT,
    post_id BIGINT,
    type ENUM('like', 'comment') NOT NULL,
    read BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES User(id) ON DELETE CASCADE,
    FOREIGN KEY (post_id) REFERENCES Post(id) ON DELETE CASCADE
);




