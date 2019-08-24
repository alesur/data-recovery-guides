## Windows Command to retain all permisions, ownership and timestamps of the entire folder structure and data while copying from place to other:


robocopy source destination /E /ZB /DCOPY:T /COPYALL /R:1 /W:1 /V /TEE /LOG:Robocopy.log

**What the switches mean:**

source :: Source Directory (drive:\path or \\server\share\path).
destination :: Destination Dir  (drive:\path or \\server\share\path).
/E :: copy subdirectories, including Empty ones.
/ZB :: use restartable mode; if access denied use Backup mode.
/DCOPY:T :: COPY Directory Timestamps.
/COPYALL :: COPY ALL file info (equivalent to /COPY:DATSOU).  Copies the Data, Attributes, Timestamps, Ownser, Permissions and Auditing info
/R:n :: number of Retries on failed copies: default is 1 million but I set this to only retry once.
/W:n :: Wait time between retries: default is 30 seconds but I set this to 1 second.
/V :: produce Verbose output, showing skipped files.
/TEE :: output to console window, as well as the log file.
/LOG:file :: output status to LOG file (overwrite existing log).
