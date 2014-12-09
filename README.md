## Description

This project is in developement phase and is created with aim to process incoming streams from the message emitter in real time. It has two applications job_tracker and stream_processing. Stream_processing app depends on the job_tracker app,so prior to starting the stream_processing app,the job_tracker app needs to be started. Job_tracker application has a process named job_tracker_procs, it passes the module_name,start function name and function arguments to the scenario supervisor of stream processing app, so that it can dynamically start the child processes namely spout_procs, filter_bolt, count_bolt. Spout_procs reads input from the input.txt file and passes the read msg to the filter_bolt. filter_bolt processes the message and filters them according to the particular tag in the message. if the message contains the desired tag then it is passed on to the next bolt called count_bolt else the message is discarded. Count_bolt reads the incoming messages from the filter_bolt, write them into output.txt file and prints the amount of message it had read on the console.


## Project Layout

The Project layout of the software is as  below:
     - Each application directory must have five sub directory/Folder.
         -sub folder
              1. ebin folder - It contains compiled code and *.app file.
              2. include folder - It contains all the header files.
              3. priv folder - anything else like C executables or native objects ends up in this folder
              4. src folder - this is the directory where all our source code is placed. 
              5. test folder - it contains all the test files.
    Apart from the above folder there is an Emake file containing the script about
    how to compile and process the modules inside sub directories.

## Execution

  In the terminal write the command  erl -make 
    then write 'erl' to start the erlang emulator
    now write   make:all([load]).
    then   cd(ebin).
    then for unit testing write
          eunit:test(job_tracker_procs_test).
          eunit:test(warehouse_procs_test).
          eunit:test(job_sup_test).
    and now start the applications,
          application:start(job_tracker).
          application:start(stream_processing).
    and runthe integeration test to finally verify the result
           eunit:test(i_test).
