<?php

/**
 * PHP Mail tester
 * Written by Pedro Ladaria <Sonic1980@gmail.com> for www.hispashare.com
 *
 * This program is free software; you can redistribute it and/or
 * modify it under the terms of the GNU General Public License
 * as published by the Free Software Foundation; either version 2
 * of the License, or (at your option) any later version.
 *
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with this program; if not, write to the Free Software
 * Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA  02111-1307, USA.
 */

print(
"<?xml version=\"1.0\" encoding=\"ISO-8859-1\"?>
<!DOCTYPE html PUBLIC \"-//W3C//DTD XHTML 1.0 Transitional//EN\" \"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd\">
<html xmlns=\"http://www.w3.org/1999/xhtml\" xml:lang=\"en\" lang=\"es\">
<head><title>PHP Mail tester - Checks if an email account is valid (asking to the mail server).</title>
<body>
<style>body { padding:0px 40px;background:#fff; color:#000; font-family:monospace; font-size:10pt; }</style>
<h1>PHP Mail tester</h1>
<form method=\"get\" action=\"\">
Enter an email
<input type=\"text\" name=\"email\" value=\"{$_GET['email']}\"> 
<input type=\"submit\">
</form>
");

function debug($s) { print(nl2br(htmlspecialchars($s))."<br/>\n"); flush(); }

function freadu($fp,$u) {
  $s = fread($fp, 4096);
  $l = strlen($u);
  while (substr($s, -$l)!==$u) $s.=fread($fp,4096);
  return $s;
}

function mailcommand($fp, $command, $debug=false) {
  if ($debug) print('<b>C&gt;</b>'.nl2br(htmlspecialchars($command))."<br/>\n"); 
  $code = false;
  @fwrite($fp, "$command\r\n"); 
  $s = @freadu($fp, "\r\n");
  if ($debug) print('<b>S&gt;</b>'.nl2br(htmlspecialchars($s))."<br/>\n");
  $s = explode("\n", trim($s));
  $code = substr(trim($s[count($s)-1]), 0, 3); 
  return $code;
}

function mailtest($email, $debug=false) {
/*
  if (!eregi("^[_a-z0-9-]+(\.[_a-z0-9-]+)*@[a-z0-9-]+(\.[a-z0-9-]+)*(\.[a-z]{2,4})$", $email)) { 
    if ($debug) debug("Wrong email or with invalid characters.");
    return false;
  }
*/
  list($user, $domain) = explode('@', $email);
  if ($debug) debug("Getting MX registers of domain: \"$domain\"...");

  // registros mx
  $getmxrr = getmxrr($domain, $mx_records, $mx_weights);
  if (($getmxrr==true) and (count($mx_records)>0)) {
    for ($i=0; $i<count($mx_records); $i++) $mxs[$mx_records[$i]] = $mx_weights[$i];
    asort($mxs);
    $mx_records = array_keys($mxs);
    $mx_weights = array_values($mxs);
    if ($debug) { 
      for ($i=0; $i<count($mx_records); $i++) 
        debug(" $i: {$mx_records[$i]} [{$mx_weights[$i]}]");
    }
  }
  else {    
    if ($debug) debug("None found.\nUsing domain \"$domain\" as mail server...\n");
    $mx_records[0] = $domain; // si no se obtienen regs MX, usar el mismo dominio
  }
  $return = false;
  foreach ($mx_records as $mx_host) {
    if ($debug) debug("Testing with: $mx_host...");
    $fp = @fsockopen($mx_host, 25, $fs_errn, $fs_errs, 5);
    if ($fp) {
      if ($debug) debug("Connecting to \"$mx_host\".\n");

      $s = @freadu($fp, "\r\n");
      if ($debug) print('<b>S&gt;</b>'.nl2br(htmlspecialchars($s))."<br/>\n");

      $code = mailcommand($fp, "EHLO mail_test", $debug);
      if (($code!='250') and ($code!='220')) {
        if ($debug) debug("[$code] Respuesta incorrecta\n");      
        fclose($fp);
        continue;
      }  

      $code = mailcommand($fp, "MAIL FROM:<root@hispashare.com>", $debug);
      $code = mailcommand($fp, "RCPT TO:<$email>", $debug);
      if ($debug) debug("\nCode: $code\n");
      $return = $code=='250';
      break;
    }
    else if ($debug) debug("Error [$fs_errn] connectig to \"$mx_host\": $fs_errs.");
  }

  // fin
  return $return;  
}


if (isset($_GET['email'])) {
  $email = $_GET['email'];
  print("<h2>Checking $email</h2>\n");
  if (mailtest($email, true))
    print("<h2>Email \"{$_GET['email']}\" seems to be OK</h2>");
  else
    print("<h2>Email \"{$_GET['email']}\" seems to be wrong</h2>");
}

?>

<div><br/><a href="../">Return to Index</a></div>
</body>
</html>
