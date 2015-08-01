## Notes on RMySQL

library(DBI)
con <- dbConnect(RMySQL::MySQL(), group = "my-db") # uses info in ~/.my.cnf

dbListTables(con)

# data from Managing and using MySQL, page 41
books <- data.frame(id=1:5,
                    title=c("The Green Mile", "Guards, Guards!", "Imzadi",
                            "Gold", "Howling Mad"),
                    author=c(4,2,3,1,3),
                    pages=c(894,302,354,405,294))
authors <- data.frame(id=1:5,
                      name=c("Isaac Asimov", "Terry Pratchett", "Peter David",
                             "Stephen King", "Neil Gaiman"),
                      citizen=c("US", "UK", "US", "US", "UK"))

dbWriteTable(con, "books", books)
dbWriteTable(con, "authors", authors)
dbListTables(con)

dbListFields(con, 'books')
dbColumnInfo(con, 'books')

dbReadTable(con, "books")

# simple query
res <- dbSendQuery(con, "SELECT * FROM books WHERE author = 3")
dbFetch(res)
dbClearResult(res) # <- important to do this when done with query

# inner join
res <- dbSendQuery(con, paste("SELECT books.title, authors.name",
                              "FROM authors, books",
                              "WHERE books.author = authors.id",
                              "ORDER BY authors.id, books.title"))
dbFetch(res)
dbClearResult(res)

dbDisconnect(con)
