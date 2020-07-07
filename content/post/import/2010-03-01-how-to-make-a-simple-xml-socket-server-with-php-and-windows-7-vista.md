---
title: How to make a Simple XML Socket Server with PHP and Windows 7 / Vista
author: ETdoFresh
type: post
date: 2010-03-01T21:47:00+00:00
url: /how-to-make-a-simple-xml-socket-server-with-php-and-windows-7-vista/
blogger_blog:
  - etdofresh.blogspot.com
blogger_author:
  - ETdoFresh
blogger_permalink:
  - /2010/03/how-to-make-simple-xml-socket-server.html
blogger_internal:
  - /feeds/8161366669954270448/posts/default/8619297353213293907
categories:
  - Uncategorized

---
<div xmlns='http://www.w3.org/1999/xhtml'>
  <p>
    Dear Blog,
  </p>
  
  <p>
    Today we are going to discuss how make a simple XML socket server using PHP (as a command line server) and Flash as the client. I assume that PHP has been installed with the &#8220;sockets plug-in&#8221;.
  </p>
  
  <p>
    First let&#8217;s associate a new type of file to Windows, called PHS, or PHP Script. (I borrowed the following from <a href="http://www.php.net/manual/en/features.commandline.php#93479">this site</a>) Open up a command prompt window and&#8230;
  </p>
  
  <pre>ASSOC .phs=PHPScript
FTYPE PHPScript=[path to]php.exe -f "%1" -- %*
set PATHEXT=.phs;%PATHEXT%</pre>
  
  <p>
    Now evertime you click on a phs file, it should open up in PHP CLI (Command Line Interface).
  </p>
  
  <p>
    After that, we simply create a PHS like the following that will run as your server (borrowed from <a href="http://devzone.zend.com/article/1086#Heading7">here</a> and tweaked to work <a href="http://wheresninja.com/sxmlss/simpleXMLSocketServer.phps">here</a>)&#8230;
  </p>
  
  <pre>&lt;?php 
echo "Starting XML Socket Servern";

// Set time limit to indefinite execution 
set_time_limit (0); 

// Set the ip and port we will listen on 
$address = 'localhost'; 
$port = 9001; 
$max_clients = 10; 

// Array that will hold client information 
$client = array(); 

// Create a TCP Stream socket 
$sock = socket_create(AF_INET, SOCK_STREAM, 0); 
// Bind the socket to an address/port 
socket_bind($sock, $address, $port) or die('Could not bind to address'); 
// Start listening for connections 
socket_listen($sock); 

// Loop continuously 
while (true) { 
    // Setup clients listen socket for reading 
    $read[0] = $sock; 
    for ($i = 0; $i &lt; $max_clients; $i++) 
    { 
        if (isset($client[$i]) && $client[$i]['sock'] != NULL) {
            $read[$i + 1] = $client[$i]['sock'] ; 
  }
    } 
    // Set up a blocking call to socket_select()
 $temp = array();
    $ready = socket_select($read,$temp,$temp,NULL); 
    /* if a new connection is being made add it to the client array */ 
    if (in_array($sock, $read)) { 
        for ($i = 0; $i &lt; $max_clients; $i++) { 
   if (!isset($client[$i])) { 
                $client[$i]['sock'] = socket_accept($sock); 
                break; 
            } 
            elseif ($i == $max_clients - 1) {
                print ("too many clients") ;
   }
        }
        if (--$ready &lt;= 0) {
            continue; 
  }
    } // end if in_array 
     
    // If a client is trying to write - handle it now 
    for ($i = 0; $i &lt; $max_clients; $i++) { // for each client
  if (isset($client[$i])) {
         if (in_array($client[$i]['sock'] , $read)) { 
             $input = socket_read($client[$i]['sock'] , 1024); 
             if ($input == NULL) { 
                 // Zero length string meaning disconnected 
                 unset($client[$i]); 
             } 
             $n = trim($input); 
             if ($input == 'exit') { 
                 // requested disconnect 
                 socket_close($client[$i]['sock']); 
             } elseif ($input) { 
     echo "Client $i sends:n$inputnn"; 
                 // strip white spaces and write back to user 
                 $output = ereg_replace("[ tnr]","",$input).chr(0); 
                 socket_write($client[$i]['sock'],$output); 
             } 
         } else { 
             // Close the socket 
             socket_close($client[$i]['sock']); 
             unset($client[$i]); 
         }
  }
    } 
} // end while 
// Close the master sockets 
socket_close($sock); 
?&gt;</pre>
  
  <p>
    Double click that file, and you should have an XML Socket Server that repeats whatever you send it.
  </p>
  
  <p>
    Now open up flash, and have it connect and send something to the server. If everything works, you should see the response in the trace portion of your flash window. Done! (I included the Flash file I made <a href="http://wheresninja.com/sxmlss/sxmlss.fla">here</a>).
  </p>
  
  <p align='center'>
    <a href=""><img height="149" width="288" src="" /></a>
  </p>
  
  <p>
    Hope this helps someone in cyber-world!
  </p>
  
  <p>
    &#8211; ETdoFresh
  </p>
</div>