# PHP-Filechange-Tracker
 PHP class to track changes of files based on modification time

## Usage

```php
$filetracker = new filechangeTracker();

$filetracker->addmonitor( "/tmp/track/file1", "functionOnChange1");
$filetracker->addmonitor( "/tmp/track/file2", "functionOnChange_Other");
$filetracker->addmonitor( "/tmp/track/file3", "functionOnChange_Other");

// You may also remove a monitor on-the-fly
$filetracker->removemonitor( "/tmp/track/file4");


while(1) {
    $numchanged = $filemonitor->check();
    echo "$numchanged files have changed\n";
    sleep(1);
}

function functionOnChange1( $filename, $mtime ) {
    echo "File changed: $filename\n";

    if( $mtime == false ) {
        echo "File does not exist\n";
    } 
    else {
        echo "Filetime (epoch) is $mtime\n";
        // Do something with the file, e.g. read config from it
    }
}

function functionOnChange_Other ( $filename, $mtime ) {
    // You may also use the same callback with different files
    // You can decide what to do inside of your function
    if( $filename == "/tmp/tracke/file2" ) {
        // Do this
    }
    else { 
        // Do that
    }
}
```

## Return values / exceptions

- The new constructor returns the filemonitor object
- The addmonitor and removemonitor return nothing
- addmonitor throws an exception, if the functionname does not exist in your program
- check returns the number of changed files in the last turn




