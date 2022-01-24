# Data Engineering ZoomCamp Homework Week 1

## Exercises 1 ##
SELECT count(1) FROM `crafty-sound-339022.zones.yellow_trips` 
where
extract(DATE from tpep_pickup_datetime) = '2021-01-15';

## Exercises 2 ##
select max(tip_amount) as max_tip, extract(DATE from tpep_pickup_datetime)  FROM `crafty-sound-339022.zones.yellow_trips` 
group by  tpep_pickup_datetime
order by max_tip desc
limit 1;

## Exercises 3 ##
select a.DOLocationID, count(1), c.Zone from `crafty-sound-339022.zones.yellow_trips` as a
inner join `crafty-sound-339022.zones.zones` as b on 
a.PULocationID = b.LocationId
inner join `crafty-sound-339022.zones.zones` as c on
a.DOLocationID = c.LocationID
group by a.DOLocationID, c.Zone
order by count(1) desc
limit 1;

## Exercises 4 ##
update `crafty-sound-339022.zones.zones`
    set Zone = 'Unknown'
    where Zone in ('NA', 'NV');

select concat(ifnull(b.Zone,'unknown'), '/', ifnull(c.Zone,'unknown')) as trip, avg(a.total_amount) as average  from `crafty-sound-339022.zones.yellow_trips` as a
inner join `crafty-sound-339022.zones.zones` as b on 
a.PULocationID = b.LocationId
inner join `crafty-sound-339022.zones.zones` as c on
a.DOLocationID = c.LocationID
group by trip
