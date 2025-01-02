-- Use database
USE daoctracking;

-- Create table announcements with full-text index
CREATE TABLE announcements (
    announcementkey INT AUTO_INCREMENT PRIMARY KEY,
    announcementtext VARCHAR(4000),
    announcementtype VARCHAR(100),
    announcementtime TIME,
    channelID BIGINT,
    mentionID VARCHAR(100),
    channelname VARCHAR(100),
    mentionname VARCHAR(100),
    FULLTEXT KEY idx_fulltext_announcements (announcementtext, announcementtype, channelname, mentionname)
) ENGINE=InnoDB;

-- Create table bloblogging
CREATE TABLE bloblogging (
    blobtrackingkey INT AUTO_INCREMENT PRIMARY KEY,
    `blob` TEXT,
    secondblob TEXT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- Create table characterrealmstats
CREATE TABLE characterrealmstats (
    characterrealmstatskey INT AUTO_INCREMENT PRIMARY KEY,
    character_web_id VARCHAR(400),
    realmpoints INT,
    bountpoints INT,
    totalkills INT,
    totaldeaths INT,
    totaldeathblows INT,
    totalsolokills INT,
    midkills INT,
    middeathblows INT,
    midsolokills INT,
    hibkills INT,
    hibdeathblows INT,
    hibsolokills INT,
    albkills INT,
    albdeathblows INT,
    albsolokills INT,
    importdate DATE,
    lifetimeIRS DECIMAL(15, 2) GENERATED ALWAYS AS (IF(totaldeaths = 0, realmpoints, realmpoints / totaldeaths)) STORED,
    dailyrealmpoints INT,
    dailydeaths INT,
    dailyIRS DECIMAL(15, 2) GENERATED ALWAYS AS (IF(dailydeaths = 0, dailyrealmpoints, dailyrealmpoints / dailydeaths)) STORED,
    lastrecordflag INT
);

-- Create table characters with full-text index
CREATE TABLE characters (
    characterskey INT AUTO_INCREMENT PRIMARY KEY,
    character_web_id VARCHAR(200),
    name TEXT,
    firstname TEXT,
    server_name TEXT,
    archived TEXT,
    realm INT,
    race TEXT,
    class_name TEXT,
    level INT,
    last_on_range INT NOT NULL,
    realm_points INT,
    guild_rank INT,
    guild_web_id VARCHAR(100),
    watchlistflag BOOLEAN DEFAULT FALSE,
    lastupdated DATETIME,
    FULLTEXT KEY idx_fulltext_characters (name, firstname, server_name, archived, race, class_name)
) ENGINE=InnoDB;


-- Create table commands
CREATE TABLE commands (
    commandskey INT AUTO_INCREMENT PRIMARY KEY,
    commandtext VARCHAR(200),
    FULLTEXT KEY idx_fulltext_commands (commandtext)
) ENGINE=InnoDB;

-- Create table guilds
CREATE TABLE guilds (
    guildskey INT AUTO_INCREMENT PRIMARY KEY,
    guild_web_id VARCHAR(100),
    guildname VARCHAR(2000),
    importedflag BOOLEAN,
    FULLTEXT KEY idx_fulltext_guilds (guildname)
) ENGINE=InnoDB;

-- Create table guilds_importedfalse
CREATE TABLE guilds_importedfalse (
    guildskey INT AUTO_INCREMENT PRIMARY KEY,
    guild_web_id VARCHAR(100),
    guildname VARCHAR(2000),
    importedflag BOOLEAN
) ENGINE=InnoDB;

-- Create table realmranks
CREATE TABLE realmranks (
    realmrankskey INT AUTO_INCREMENT PRIMARY KEY,
    realmrank VARCHAR(10),
    realmpoints INT
);

-- Create table User
CREATE TABLE User (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username NVARCHAR(80) NOT NULL UNIQUE,
    email NVARCHAR(120) NOT NULL UNIQUE,
    password_hash NVARCHAR(120) NOT NULL,
    FULLTEXT KEY idx_fulltext_user (username, email)
) ENGINE=InnoDB;

-- Create table UserCharacterXref
CREATE TABLE UserCharacterXref (
    usercharacterxrefkey INT AUTO_INCREMENT PRIMARY KEY,
    character_web_id NVARCHAR(200) NOT NULL,
    userid INT
);

-- Add constraints and indexes
CREATE INDEX idx_character_name ON characters (character_web_id, name(255));
CREATE INDEX idx_character_web_id ON characterrealmstats (character_web_id);
CREATE INDEX idx_guild_web_id ON guilds (guild_web_id);
