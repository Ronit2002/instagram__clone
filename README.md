Very basic instagram clone-It can find the oldest users,identify users who have not uploaded any photos,It can identify most popular photos and user to whom it belong to ,It can identify the most popular registeration day,It can identify how many times does an average user posts and the most popular tags.





create database ig_clone;
use ig_clone;
create table users(
	id int auto_increment primary key,
    username varchar(255) unique not null,
    created_at timestamp default now()
);

insert into users(username) values
("Ronit"),
("Rahul"),
("Rishi");

create table photos(
	id int auto_increment primary key,
    image_url varchar(255) not null,
    user_id int not null,
    created_at timestamp default now(),
    foreign key(user_id) references users(id)
);

insert into photos(image_url,user_id)values
('/asdf',1),
('/addf',2),
('/asef',2);

create table comments(
	id integer auto_increment primary key,
    comment_text varchar(255) not null,
    user_id int not null,
    photo_id int not null,
    created_at timestamp default now(),
    foreign key(user_id) references users(id),
    foreign key(photo_id) references photos(id)
);

insert into comments(comment_text,user_id,photo_id)values
('Hello',1,2),
('World',1,1);

create table likes(
	user_id int not null,
    photo_id int not null,
    created_at timestamp default now(),
	foreign key (user_id) references users(id),
    foreign key(photo_id) references photos(id),
	primary key(user_id,photo_id)
);

insert into likes(user_id,photo_id)values
(1,2),
(1,1);

create table follows(
	follower_id int not null,
    followee_id int not null,
    created_at timestamp default now(),
    foreign key(follower_id) references users(id),
    foreign key(followee_id) references users(id)
);

insert into follows(follower_id,followee_id)values
(1,2),
(1,3);

create table tags(
	id int auto_increment primary key,
    tag_name varchar(255) unique,
    created_at timestamp default now()
);

create table photo_tags(
	photo_id int not null,
    tag_id int not null,
    foreign key(photo_id) references photos(id),
    foreign key(tag_id) references tags(id),
    primary key(photo_id,tag_id)
);

insert into tags(tag_name)values
('heljfds'),
('hdsuhdu');

insert into photo_tags(photo_id,tag_id)values
(1,1),
(2,2);

select * 
from users 
order by created_at 
limit 5;

select 
dayname(created_at) as day,
count(*) as total 
from users
group by day
order by total desc; 

select username
from users
left join photos
on users.id=photos.user_id
where photos.id is null;


select username,
photos.id,
photos_url,
count(*) as total
from photos
inner join likes 
on likes.photo_id=photos.id
inner join users
on photos.user_id=users.id
group by photos.id
order by total desc
limit 1;

select 
(select count(*) from photos)/(select count(*) from users);

select tag.tag_name,
count(*) as total
from photo_tags
join tags
on photo_tag.tag_id=tags.id
group by tag.id
order by total desc
limit 5;
