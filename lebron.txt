from urllib.request import urlopen as uReq
from bs4 import BeautifulSoup as soup
import time
my_url="https://www.basketball-reference.com/players/j/jamesle01/gamelog-playoffs/"
read_url=uReq(my_url)
uClient=read_url.read()
read_url.close()

page_soup=soup(uClient, "html.parser")
#stats=page_soup.find_all("tr")
#print(stats[36].text)
#headers_2006=stats[36].text
headers="Date, Series, Team, Opponent, Game#, Result, Games Started, Min played, FG, FGA, FG%, 3P, 3PA, 3P%, FT, FTA, FT%, OReb, DReb, TReb, Assists, Steals, Blocks, TOV, PF, Points, GmSc, +/-\n"
f=open("lebron.csv","w")
f.write("Lebron James\n")
f.write(headers)




lebron=page_soup.find("tbody")
stat1=lebron.find_all("tr")
#print(stat1)
#print('-------------------------')
#print(stat1[0])
#print("==========================")
#print(stat1[1])

lebron=page_soup.find("tbody")
stat1=lebron.find_all("tr")
for stat in stat1:
	if stat.a==None:
		continue;
	date=stat.a.text
	print("date:",date)
	a=stat.find_all("a")
	b=stat.find_all("td",{"class": "center"})
	c=stat.find_all("td",{"class":"right"})
	series=a[1].text
	print("series:",series)
	team=a[2].text
	print("team:",team)
	opp=a[3].text
	print("Opponent:",opp)
	game_num=a[4].text
	print("Game number:",game_num)
	result=b[3].text
	print("Game result:",result)
	games_started=c[1].text
	print("Games started:",games_started)
	minutes_played=c[2].text
	print("Minutes played:",minutes_played)
	fg=c[3].text
	print("Field goal:",fg)
	fga=c[4].text
	print("Field goal attempts:", fga)
	fg_percent=c[5].text
	print("Field goal percentage", fg_percent)
	fg_3=c[6].text
	print("3 pointers made:", fg_3)
	fg_3a=c[7].text
	print("3 pointers attempted:",fg_3a)
	fg_3_percent=c[8].text
	print("3 point percentage:", fg_3_percent)
	ft=c[9].text
	print("Free throws made:",ft)
	fta=c[10].text
	print("Free throws attempted:", fta)
	ft_percent=c[11].text
	print("Free throw percentage:",ft_percent)
	oreb=c[12].text
	print("Offensive rebounds:", oreb)
	dreb=c[13].text
	print("Defensive rebounds:", dreb)
	treb=int(oreb)+int(dreb)
	print("Total rebounds:", treb)
	assists=c[15].text
	print("Assists:", assists )
	steals=c[16].text
	print("Steals:", steals)
	blocks=c[17].text
	print("Blocks:", blocks)
	tov=c[18].text
	print("TOV:", tov)
	pf=c[19].text
	print("Personal fouls:", pf)
	points=c[20].text
	print("Points scored:", points)
	game_score=c[21].text
	print("Game score:", game_score)
	plus_minus=c[22].text
	print("Plus_minus:", plus_minus)
	print("--------------------------")
	f.write(date + "," + series + "," + team + "," + opp + "," + game_num + "," + result + "," + games_started + ","  + minutes_played + "," + fg + "," + fga + "," + fg_percent + "," + fg_3 + "," +
	fg_3a + "," + fg_3_percent + "," + ft + "," + fta + "," + ft_percent + "," + oreb + "," + dreb + "," + str(treb) + "," + assists + "," + steals + "," +
	blocks + "," + tov + "," + pf + "," + points + "," + game_score + "," + plus_minus + "\n")


f.close()

time.sleep(1)