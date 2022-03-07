# Highest_Energy_Consumption
solution
select date,total_energy
from
(SELECT date,SUM(consumption) as total_energy,rank() over(order by SUM(consumption) DESC) as r
from
(select * from fb_eu_energy
UNION ALL
select * from fb_asia_energy
UNION ALL
select * from fb_na_energy) fb_energy
group by date)fb_ranked
where r=1
