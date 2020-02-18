---
layout: post
title: Converting an SQLite database to PostgreSQL
date: 2020-02-12
---

Using the same base code/files, the Todo Flask app now works for PostgreSQL using pysopg2.

Key changes/differences:
- Wrote a function to run a query, rather than writing the same few lines inside each function within the helper file
- String arguments must be indicated with `%s`, whereas previously `?` was used
- SQLite allowed for a simple path specification; psycopg2 needed a much more specific path laid out
- psycopg2 requires the connection to be closed when you're finished with it

Most of the time on this project was spent debugging, as a majority of the code was already written and ready to go with the SQLite app- most, if not all, changes were done within the helper file. The major takeaway was to insert `print()` lines throughout the code to determine where exactly the issues were, as the terminal didn't always specify.