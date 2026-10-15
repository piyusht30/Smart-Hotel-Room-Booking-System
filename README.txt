SMART HOTEL / HOSTEL ROOM BOOKING SYSTEM  -  PROJECT FOLDER
===========================================================

FOLDER CONTENTS
  hotel_booking_system.py     Complete application (Python + Streamlit + SQLite)
  database/                   Backend: pure SQL files and a ready database
      01_schema.sql           7 tables, keys, constraints, 3 triggers, 2 views
      02_sample_data.sql      Sample customers, rooms, bookings, payments, feedback
      03_queries.sql          9 demo queries (joins, group by, subqueries, view)
      04_trigger_demo.sql     Shows the 3 triggers working
      hotel_backend.db        Ready SQLite database (schema + sample data)
  presentation_DBMS/          PPT for the DBMS subject
  presentation_ML/            PPT version that also covers the ML part
  report/                     Put your exported report here


A) RUN THE APPLICATION  (Mac: use python3)
  1. Open this folder in VS Code (File > Open Folder).
  2. Open the terminal (Terminal > New Terminal) and run:
        python3 -m pip install streamlit pandas numpy scikit-learn
        python3 -m streamlit run hotel_booking_system.py
  3. The browser opens at http://localhost:8501  (wait up to 1 minute at first).
  The app creates its own file "hotel.db" the first time it runs.
  To reset the data, press Ctrl + C, delete hotel.db and run again.


B) SHOW THE DATABASE BACKEND  (no Python needed)
  Mac already has sqlite3. In the terminal:
        cd database
        sqlite3 hotel_backend.db < 03_queries.sql
        sqlite3 hotel_backend.db < 04_trigger_demo.sql
  Or open database/hotel_backend.db in "DB Browser for SQLite"
  (free, sqlitebrowser.org) and click through the tables.

  To rebuild the database from scratch:
        cd database
        rm -f hotel_backend.db
        sqlite3 hotel_backend.db < 01_schema.sql
        sqlite3 hotel_backend.db < 02_sample_data.sql
  (If "sqlite3" is not found, use DB Browser for SQLite and run the .sql files
   from its "Execute SQL" tab.)


DATABASE SUMMARY
  Tables   : Customer, RoomType, Room, Staff, Booking, Payment, Feedback
  Triggers : trg_checkin        -> room becomes Occupied on check-in
             trg_release_room   -> room becomes Available on check-out / cancel
             trg_cancel_count   -> customer's cancellation count +1 on cancel
  Views    : v_occupancy, v_booking_details
  Bill     : nights x price per night x 1.12 (12% GST)
