![alt text](/rowing.png)

# ETL of Rowing Regattas data

_Disclaimer:_This project uses public data, available at www.worldrowing.com. The use of this information has the sole purpose to show my data science skills, and also education purposes. All procedures presented here comply with fair use of public information.  


**Background**  
Rowing is an Olympic sport where races are contested over a six-lane, 2000m-long straight course. Since there are only six lots available to race for the gold medal, the final (named Final A) is preceded by a series of qualifying rounds of heats, quarter-finals, and semi-finals (the quantity of each stage depends on the number of boat entries in that race. E.g. If there are 6 boats, the progression will be different compared to 60 boats). The results of these qualifying races finals (B, C, D, and so forth) that  determine the placement (ranking) in the competition. In addition to this complex progress system, Rowing also features different boat classes including whether the athlete uses a single or a pair of oars to propel the boat, the number of crew members vary (single, double, four, and eight athletes), the athlete is heavy or lightweight, and the athlete is a woman or a man. As a result, what appears to be a simple sport: move a boat using oars! Is actually a very complex one, when it comes to competition. Therefore, analysing the data of rowing competitions may lead to interesting insights for the athletes, coaches and staff that work on improving performance.  


**Scenario**  
The World Rowing organizes World Championships every year, for each age category (U19 - athletes younger than 18 years of age, formerly known as Juniors; U23 - athletes younger than 23 years of age; and Senior - open age category). There is an ongoing release of racing documentation during these events and, at the end, all the files are made available for download in the World Rowing website. It is unfortunate, however, that all these data are stored in PDF format, which make it dificult process in large volumes such as all the race in these events. For example, at the 2022 Senior World Championships 256 races were distributed over eight days. Each race derive three different files being:  

* Media Start List: this file stores information on the final, race number, boat class, weight class, sex, race time, race date, athlete names, the lane they are racing, their country, their date of birth;  
* Race data: this file stores information on the final, race number, boat class, weight class, sex, race time, race date, the rank, the lane, their country, boat velocity and stroke rate at every 50m of the race (40 splits);
* Results: this file stores information on the final, race number, boat class, weight class, sex, race time, race date, athlete names, the rank, the lane they are racing, their country, their seat position in the boat, the accumulated performance duration for 500m, 1000m, 1500m, and 2000m;  

To process all these data quickly, one should either use the original files, produced in spreadsheets or use scripts that extract the data from the PDF files, organize them as a table and save in a .csv format for analysis. Therefore, for this project I aimed to optimize the collection of the data from the provided PDF and pre-processed them, organizing each file and merging them into a single data frame.  

**Case Study Roadmap**  

**Ask**  
The question that guided this project was:  

* How do I optimize the wrangling of Rowing World Championships data?  


**Prepare**  

A webpage stores the PDFs used in this project in separate links (by race) in .PDF files. The data in the PDFs are collected by the racing organizers using electronic timing system as well as electronic units that possess GPS and accelerometers that derive boat velocity and stroke rate. Assuming the data come from these systems, any existing bias may come from either equipment or system error and may be systematic. World Rowing made the data available for download at their website. After downloading, the data was stored in a physical drive (external hard drive) protected by password.  


**Process**  

For this project, I have used the following tools:  

* Python 3.10.4;
* Pandas 1.5.2;
* pdfplumber 0.7.6;
* Numpy 1.24.1;  


This project deals with three different PDF files, where, although related to the same race, each one carries different information about the same crews. Therefore, each PDF "type" was treated in separate and merged at the end of the process. For example, the media start list files had the date of birth of the rowers whereas the other information were also on the other PDF types. Therefore, the notebook has the code separated by file types.  

There was a common way that all the PDFs were treated. See below the general workflow for data extraction:  
1. First, the directory where the PDFs were was identified;
2. The type of file extension the code should look for was established;  
3. Then, a function to collect the heading data from the PDFs was created. This function identifies the races;  
4. A loop for iterates over the list of files, opens it, detects whether the file belongs to single, double, four, or eight people boat, process the information of interest, and saves it in a .csv file in a directory previously determined.  

These procedures were performed in all files. A limitation of this project was that not all the PDF files had the exact same pattern. This means that even though this project optimized the ETL process for Rowing World Championship data, a few times I had to locate and adjust the code to collect the correct information, were the slicing picked up the incorrect information due to its postition.  

**Conclusion**  

Handling real-world data can be a dauting task, due to lack of structure, and pattern of the sources. Implementing optimizing tools should help in the process and make the work flow efficient.
