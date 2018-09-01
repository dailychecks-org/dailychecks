Data model
==========

(WIP, none of this is implemented yet)

Assuming that users have their own individual storage space,
the model elements do not to have an explicit owner,
the owner is implied by the currently logged in user.


Habits
------

Habits to include in listings, and their details.

Fields:

- name
  - mutable

- type: positive or negative
  - example: jogging is a positive habit to be encouraged
  - example: smoking is a negative habit to be discouraged
  - immutable

- frequency: the target frequency in days (minimum for positive, maximum for negative)
  - example: jogging every 3 days or more
  - example: smoking every 4 days or less
  - mutable

- technical fields: id, date of creation
  - immutable


HabitLogs
---------

All the dates when habits were performed.

Fields, all immutable:

- habit

- date


LastHabitLogs
-------------

The last date when each habit was performed.

Same fields as in HabitLogs. Ideally a view over HabitLogs.


HabitStats
----------

Various pre-computed stats over HabitLogs,
to reduce the complexity and to speed up client applications.

Fields: TODO


Settings
--------

User settings, such as timezone.

Fields: TODO
