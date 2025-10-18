#Query1:What are the average IMDb scores for each genre of Netflix Originals?
        SELECT Genre_details.Genre, AVG(Netflix_originals.IMDBScore) AS Avg_imdb
        FROM Netflix_originals
        JOIN Genre_details
        ON Netflix_originals.GenreID = Genre_details.GenreID
        GROUP BY Genre_details.Genre;
#Query2:Which genres have an average IMDb score higher than 7.5?
        SELECT Genre_details.Genre, AVG(Netflix_originals.IMDBScore) AS Avg_imdb
        FROM Netflix_originals 
        JOIN Genre_details
        ON Netflix_originals.GenreID = Genre_details.GenreID  
        GROUP BY Genre_details.Genre
        Having Avg_imdb>7.5;
#Query3: List Netflix Original titles in descending order of their IMDb scores?
         Select Title,IMDBScore 
         From Netflix_Originals 
         Order By IMDBScore desc;
#Query4: Retrieve the top 10 longest Netflix Originals by runtime?
         Select Title,Runtime 
         From Netflix_Originals 
         Order By Runtime desc
         Limit 10;
#Query5: Retrieve the titles of Netflix Originals along with their respective genres?
         Select GD.Genre, NO.Title 
         From Netflix_Originals AS NO
         JOIN Genre_details AS GD
         ON NO.GenreID=GD.GenreID;
#Query6: Rank Netflix Originals based on their IMDb scores within each genre?
         SELECT GD.Genre,NO.IMDBScore,
         RANK() OVER(Partition by GD.Genre ORDER BY IMDBScore Desc) AS ranking
         FROM Netflix_Originals AS NO
         JOIN Genre_details AS GD
         ON NO.GenreID=GD.GenreID
         ORDER BY GD.Genre, ranking;
#Query7:Which Netflix Originals have IMDb scores higher than the average IMDb score of all titles?
        SELECT Title,IMDBScore 
        From Netflix_Originals 
        Where IMDBScore>(SELECT AVG(IMDBScore) from Netflix_Originals);
#Query8:How many Netflix Originals are there in each genre?
        SELECT GD.Genre,COUNT(NO.TITLE) AS NUMBER
         FROM Netflix_Originals AS NO
         JOIN Genre_details AS GD
         ON NO.GenreID=GD.GenreID
         GROUP BY GD.GENRE;
#Query9:Which genres have more than 5 Netflix Originals with an IMDb score higher than 8?
        SELECT GD.Genre,COUNT(NO.Title) AS COUNT 
        FROM Netflix_Originals AS NO
        JOIN Genre_details AS GD
        ON NO.GenreID=GD.GenreID
        WHERE IMDBScore >8
        GROUP BY GD.Genre
        Having COUNT(NO.Title)>5;
#Query10:What are the top 3 genres with the highest average IMDb scores, and how many Netflix Originals do they have?
         SELECT GD.Genre, AVG(NO.IMDBScore) AS Avg_IMDB, COUNT(NO.Title) AS Total_Originals
         FROM Netflix_Originals AS NO
         JOIN Genre_details AS GD
         ON NO.GenreID = GD.GenreID
         GROUP BY GD.Genre
         ORDER BY Avg_IMDB DESC
         LIMIT 3;

       

         
