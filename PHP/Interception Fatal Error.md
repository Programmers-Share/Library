Catch是攔截不到Error等級的，必須向PHP註冊發生Error後要呼叫的函式

以下程式碼貼到PHP中即可使用，限制版本5.2+

```php
    register_shutdown_function("fatal_handler");
    
    function fatal_handler() {
        $error = error_get_last();
        if( $error !== NULL) {
            $errno   = $error["type"];
            $errfile = $error["file"];
            $errline = $error["line"];
            $errstr  = $error["message"];

            echo (format_error( $errno, $errstr, $errfile, $errline));
        }
    }

    function format_error($errno, $errstr, $errfile, $errline) {
        $trace = print_r( debug_backtrace( false ), true );

        $content = "
            <table border='1'>
                <thead>
                    <th>Item</th>
                    <th>Description</th>
                </thead>
                <tbody>
                    <tr>
                        <th>Error</th>
                        <td><pre>$errstr</pre></td>
                    </tr>
                    <tr>
                        <th>Errno</th>
                        <td><pre>$errno</pre></td>
                    </tr>
                    <tr>
                        <th>File</th>
                        <td>$errfile</td>
                    </tr>
                    <tr>
                        <th>Line</th>
                        <td>$errline</td>
                    </tr>
                    <tr>
                        <th>Trace</th>
                        <td><pre>$trace</pre></td>
                    </tr>
                </tbody>
            </table>
        ";

        return $content;
    }
```
