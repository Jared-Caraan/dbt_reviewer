## clean_stale macro

The purpose of this macro is to:

1. queries the information schema of a database
2. finds objects that are > 1 week old (no longer maintained)
3. generates automated drop statements
4. has the ability to execute those drop statements
