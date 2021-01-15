https://docs.google.com/document/d/12-fuxHCodTHYEch_3JKTZgkD55aSSrOHKyhgjvMZk14/edit?ts=5fce5048#heading=h.my2zh5u9p9vr

# perfect-panel
Тестовое задание для Perfect Panel


select distinct u.id as ID, CONCAT(u.first_name, ' ', u.last_name) as Name, b1.author as Author, GROUP_CONCAT(b1.name)
from (
  select user_id, count(book_id) as c
  from user_books as ubc
  group by user_id
  having c = 2) as c
inner join user_books as ub_1 on ub_1.user_id = c.user_id
inner join user_books as ub_2 on ub_2.user_id = c.user_id AND ub_1.id != ub_2.id
inner join users as u on c.user_id = u.id
inner join books as b1 on ub_1.book_id = b1.id
inner join books as b2 on ub_2.book_id = b2.id
where b1.author = b2.author
group by u.id
