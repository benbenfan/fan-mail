## Database Header
C:\Data> mysql –u <username> -p
create database fanmail

## Create Table
mysql -u root -p --local-infile fanmail
SET GLOBAL local_infile = 1;

CREATE TABLE users (
    user_id BIGINT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(45) NOT NULL,
    password VARCHAR(45) NOT NULL,
    isAdmin TINYINT NOT NULL DEFAULT 0,
    email VARCHAR(45),
    handle VARCHAR(45) NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE logs (
    `time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ,
    `user_id` BIGINT UNSIGNED NOT NULL REFERENCES users(user_id),
    `line_text` TEXT NOT NULL,
    `room_id` VARCHAR(45) NOT NULL DEFAULT 0000 REFERENCES chatrooms(room_id),
    `chat_id` VARCHAR(45) NOT NULL PRIMARY KEY
);

CREATE TABLE chatrooms (
    `room_id` VARCHAR(45) NOT NULL DEFAULT 0000,
    `room_name` VARCHAR(45) NOT NULL
);

## Load Data
load data local infile './logs.csv' into table logs fields terminated by ',' lines terminated by '\r\n';

## Test Queries
INSERT INTO `users` (`user_id`, `username`, `password`, `isAdmin`, `email`, `handle`,`created_at`) VALUES('291582651', 'John Cena', 'kJFDLci81lzldeuigkja', '1', 'john.cena[at]fanfamily.org', 'johnCena', NOW());

INSERT INTO `logs`(`time`,`user_id`,`line_text`,`room_id`,`chat_id`) VALUES (NOW(),"242518965","where is everyone?","0000","9999");