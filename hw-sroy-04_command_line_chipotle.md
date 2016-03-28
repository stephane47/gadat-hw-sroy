# HW due 3/28

##Command Line Tasks

1. Look at the head and the tail of chipotle.tsv in the data subdirectory of this repo. Think for a minute about how the data is structured. What do you think each column means? What do you think each row means? Tell me! (If you're unsure, look at more of the file contents.)
    
      - This is a tab-separated table containg information about multiple orders. Column titles (5) are in the first line of the file.
      - Each order has a unique ID ('order_id', 1st column), and may consist of multiple items, each represented by a single row.
      - Multiple identical items may be listed on a single line, indicated by the 'quantity' column.
      - The 'item_name' column appears to be a set of values that corresponds directly to menu items
      - The 'choice_description' column potentially adds additional info about how each item was customized. 
        * Usually a comma separated list of strings enclosed in brackets. [one, two, three]
        * Can have nested values [Item1,[Item2,Item3,etc]]
        * Can be NULL (not blank)
      - Final column is the 'item_price'
      
    ```
    mbp13:data stephane$ head chipotle.tsv 
    order_id	quantity	item_name	choice_description	item_price
    1	1	Chips and Fresh Tomato Salsa	NULL	$2.39 
    1	1	Izze	[Clementine]	$3.39 
    1	1	Nantucket Nectar	[Apple]	$3.39 
    1	1	Chips and Tomatillo-Green Chili Salsa	NULL	$2.39 
    2	2	Chicken Bowl	[Tomatillo-Red Chili Salsa (Hot), [Black Beans, Rice, Cheese, Sour Cream]]	$16.98 
    3	1	Chicken Bowl	[Fresh Tomato Salsa (Mild), [Rice, Cheese, Sour Cream, Guacamole, Lettuce]]	$10.98 
    3	1	Side of Chips	NULL	$1.69 
    4	1	Steak Burrito	[Tomatillo Red Chili Salsa, [Fajita Vegetables, Black Beans, Pinto Beans, Cheese, Sour Cream, Guacamole, Lettuce]]	$11.75 
    4	1	Steak Soft Tacos	[Tomatillo Green Chili Salsa, [Pinto Beans, Cheese, Sour Cream, Lettuce]]	$9.25 
    ```
    ```
    mbp13:data stephane$ tail chipotle.tsv 
    1831	1	Carnitas Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice, Black Beans, Cheese, Sour Cream, Lettuce]]	$9.25 
    1831	1	Chips	NULL	$2.15 
    1831	1	Bottled Water	NULL	$1.50 
    1832	1	Chicken Soft Tacos	[Fresh Tomato Salsa, [Rice, Cheese, Sour Cream]]	$8.75 
    1832	1	Chips and Guacamole	NULL	$4.45 
    1833	1	Steak Burrito	[Fresh Tomato Salsa, [Rice, Black Beans, Sour Cream, Cheese, Lettuce, Guacamole]]	$11.75 
    1833	1	Steak Burrito	[Fresh Tomato Salsa, [Rice, Sour Cream, Cheese, Lettuce, Guacamole]]	$11.75 
    1834	1	Chicken Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Pinto Beans, Guacamole, Lettuce]]	$11.25 
    1834	1	Chicken Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Lettuce]]	$8.75 
    1834	1	Chicken Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Pinto Beans, Lettuce]]	$8.75 
    ```

1. How many orders do there appear to be? **1834, from the order_id column of the last line**

  This assumes that every integer between 1834 and 1 has been used, and that the data are sorted by the order_id
  
1. How many lines are in this file? **4623**

    ```
    mbp13:data stephane$ wc -l chipotle.tsv 
    4623 chipotle.tsv
    ```
1. Which burrito is more popular, steak or chicken?
  **Chicken is more popular:**
    ```
    mbp13:data stephane$ grep "Steak Burrito" chipotle.tsv | wc -l
     368
    mbp13:data stephane$ grep "Chicken Burrito" chipotle.tsv | wc -l
     553
    ```
    
1. Do chicken burritos more often have black beans or pinto beans?
  **Black Beans**
    ```
    mbp13:data stephane$ grep "Chicken Burrito" chipotle.tsv | grep "Black Beans" | wc -l 
     282
mbp13:data stephane$ grep "Chicken Burrito" chipotle.tsv | grep "Pinto Beans" | wc -l 
     105
    ```
    
1. Make a list of all of the CSV or TSV files in the GA-SEA-DAT1 repo (using a single command). You will be working on your local repo on your laptop. Think about how wildcard characters can help you with this task.

    ```
    mbp13:repos stephane$ find GA-SEA-DAT2 -name *.[tc]sv
    GA-SEA-DAT2/data/Airline_on_time_west_coast.csv
    GA-SEA-DAT2/data/airlines.csv
    GA-SEA-DAT2/data/bank-additional.csv
    GA-SEA-DAT2/data/bikeshare.csv
    GA-SEA-DAT2/data/chipotle.tsv
    GA-SEA-DAT2/data/citibike_feb2014.csv
    GA-SEA-DAT2/data/drinks.csv
    GA-SEA-DAT2/data/drones.csv
    GA-SEA-DAT2/data/hitters.csv
    GA-SEA-DAT2/data/icecream.csv
    GA-SEA-DAT2/data/imdb_1000.csv
    GA-SEA-DAT2/data/mtcars.csv
    GA-SEA-DAT2/data/NBA_players_2015.csv
    GA-SEA-DAT2/data/ozone.csv
    GA-SEA-DAT2/data/pronto_cycle_share/2015_station_data.csv
    GA-SEA-DAT2/data/pronto_cycle_share/2015_trip_data.csv
    GA-SEA-DAT2/data/pronto_cycle_share/2015_weather_data.csv
    GA-SEA-DAT2/data/sms.tsv
    GA-SEA-DAT2/data/syria.csv
    GA-SEA-DAT2/data/titanic.csv
    GA-SEA-DAT2/data/ufo.csv
    GA-SEA-DAT2/data/vehicles_test.csv
    GA-SEA-DAT2/data/vehicles_train.csv
    GA-SEA-DAT2/data/yelp.csv
    ```

1. Count the approximate number of occurrences of the word "dictionary" (regardless of case) across all files in the GA-SEA-DAT1 repo.
    **87?**
    ```
    mbp13:repos stephane$ grep -hroi dictionary GA-SEA-DAT2 | wc -l
      87

    ```
1. Optional: Use the the command line to discover something "interesting" about the Chipotle data. Try using the commands from the "advanced" section!
    1. **Verify the order count:**

        ```
        mbp13:data stephane$ cut -f1 chipotle.tsv | sort | uniq | wc -l
        1835
        ```
        
        Yes, 1834 unique order_ids, +1 for the column names. Try to discard the column names to get the exact count without them
        
        2 ways using sed (both lines output 1834).
        
        - ```sed -n '2,$ p' chipotle.tsv | cut -f1 | sort | uniq | wc -l```
        - ```sed '1d' chipotle.tsv | cut -f1 | sort | uniq | wc -l```
    
    1. **average items per order:**
    
        ```
        mbp13:data stephane$ sed '1d' chipotle.tsv | cut -f1 | sort | uniq -c | awk '{s+=$1}END{print "total items: ",s,"\naverage items per order: ",  s/NR}'
        total items:  4622 
        average items per order:  2.52017
        ```
    1. **Top 10 orders, by number of items**
        
        1st column - # of items; 2nd column - order number
        ```
        mbp13:data stephane$ sed '1d' chipotle.tsv | cut -f1 | sort -g | uniq -c | sort -gr | head
          23 926
          14 1483
          12 205
          11 759
          11 691
          11 1786
          10 491
           9 561
           9 1660
           8 953
        ```

        Let's verify that, by trying to find all items for order #953:
        
        ```
        mbp13:data stephane$ awk '{if ($1 == 953) print $0}' chipotle.tsv 
        953	1	Barbacoa Burrito	[Fresh Tomato Salsa, [Rice, Pinto Beans, Cheese, Lettuce]]	$9.25 
        953	1	Barbacoa Bowl	[Roasted Chili Corn Salsa, [Cheese, Lettuce]]	$9.25 
        953	1	Barbacoa Burrito	[Roasted Chili Corn Salsa, [Fajita Vegetables, Rice, Cheese, Sour Cream, Lettuce]]	$9.25 
        953	1	Steak Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Guacamole]]	$11.89 
        953	1	Steak Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice, Guacamole]]	$11.75 
        953	1	Chicken Salad Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice, Pinto Beans, Cheese, Guacamole]]	$11.25 
        953	1	Carnitas Bowl	[Fresh Tomato Salsa, [Fajita Vegetables, Rice, Black Beans, Cheese, Sour Cream]]	$9.25 
        953	1	Steak Burrito	[Tomatillo Red Chili Salsa, [Rice, Lettuce]]	$9.25 
        ```
        
        Okay, looks good.
        
    1. **How about frequency distribution of order sizes?**
    
        First column: # of items in order
        
        Second column: # How many orders with that many items
        
        ```
        mbp13:data stephane$ sed '1d' chipotle.tsv | cut -f1 | sort -g | uniq -c | sort -g | awk '{print $1}' | uniq -c | awk '{print $2 " " $1}'
        1 128
        2 1012
        3 484
        4 134
        5 44
        6 14
        7 4
        8 5
        9 2
        10 1
        11 3
        12 1
        14 1
        23 1
        ```
        
    .
    
        
