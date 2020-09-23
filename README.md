<div align="center">

## Copy Protection \(LockX\) \(Copy Protection Scheme\)


</div>

### Description

A Discussion of two Copy Protection Schemes offered on PSC. Included are a patch file for the latest LockX project and one for the 'Copy Protection Scheme - A Challenge' project. Both files are a compile of the example projects provided. I then created a patch file which defeats the protection. The Patch File applier will only patch the provided files so if you want to patch a different file you need to create your own patch file. Which is as in the real world. If the Patch File applier is run a second time then the patched application will revert to the original.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |2001-12-17 20:03:20
**By**             |[Tom Brennfleck](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/tom-brennfleck.md)
**Level**          |Intermediate
**User Rating**    |4.5 (18 globes from 4 users)
**Compatibility**  |VB 6\.0
**Category**       |[Encryption](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/encryption__1-48.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[Copy\_Prote4262112172001\.zip](https://github.com/Planet-Source-Code/tom-brennfleck-copy-protection-lockx-copy-protection-scheme__1-29871/archive/master.zip)





### Source Code

LockX and Copy Protection Scheme - A Challenge <BR><BR>
I have decided to write a small copy protection article, mainly to summarise the previous
posts and to help me get my mind around the idea, which I will present towards the end of
this article.<BR><BR>
First lets look at some of the statements made previously,<BR><BR>
I will take LockX first,<BR><BR>
Statements made were - <BR>
* The system is bullet proof<BR><BR>
This is one of the comments made for the first version, I thought yes great finally
something on the protection side. Before I got the chance to have a look at the code,
version 2 came out and its 200 times more secure.<BR><BR>
One of the Statements made was - <BR>
* LockX 2.0 Software Protection is the ultimate security system <BR><BR>
I finally got some time to check the code, it took me all of 10 minutes to figure out a
way of bypassing "the most secure ActiveX control ever " yep. <BR><BR>
And then there was version 3 with the comment<BR><BR>
* LockX 3.0 Software Protection is the ultimate security system (100 times more secure
then Version 2.0).<BR><BR>
I spent about 5 minutes on version 3 and it was bypassed, my be the authors comment
should have read 100 less secure ? .<BR><BR>
Version 3.1 was not any better, so we are now at version 3.2. Ok the OCX has been
removed, but is it more secure, I don't believe so. <BR><BR>
Attached to this article is a patch file, which will patch a particular LockX protected
application. In this case the one I compiled, with this version the author can claim that
it is 1% more secure than version 3.1 but that is all. <BR><BR>
The security of any protection product that relies on the following code is cr.p!!!<BR><BR>
If .AppRegistered Then<BR>
 Do something<BR>
Else<BR>
 End<BR>
End if<BR><BR>
If the author is as he claims a cracker then I would say that he is not very good if he
cannot even crack his own software. Any cracker will see the above code and bypass it in
a matter of minutes.<BR><BR>
That brings me to the second Solution for a protection scheme "Copy Protection Scheme"
this author has at least thought about protecting software, the supplied code still has
the above structure and therefore will not work. But the implementation of the protection
scheme is sufficiently different to make me believe that he maybe on the right track. <BR><BR>
I have been thinking along similar lines for the last couple of years, but never got
around some problems. I think Guy Gervais my have just provided a possible solution.<BR><BR>
A possible Solution<BR>
Guy's Solution<BR>
In Pseudo Code we have the following from Guy's code,<BR>
1 Load security Script into the Script Control<BR>
2 Decrypt the security script<BR>
3 Run the security script<BR>
4<BR>
5 If Me.Caption = TITLE Then<BR>
6 "Sorry, key is invalid"<BR>
7 End<BR>
8 End If<BR>
9 Do Something<BR><BR>
The above is Guy's code, and that got me thinking if the security code can be placed into
a separate thread to the main program thread, my extension to the above idea is as
follows,<BR><BR>
Main Program Thread<BR>
1 Load security Script into the Script Control<BR>
2 Decrypt the security script<BR>
3 Run the security script<BR>
4<BR>
5 If .IsDemoMode Then<BR>
6 "You are In Demo Mode" // no need to end even if the app has been patched<BR>
7 elseif .IsElapsed then<BR>
8 Show Registration Screen<BR>
9 End <BR>
10 End If<BR><BR>
{the above block takes care of honest users, and at this stage we still don't care if we
have been cracked so just keep loading the program}<BR><BR>
11 Do Something<BR><BR>
{now anywhere in the program we do the following, form load or form activate, etc.)<BR><BR>
12 Start Security Thread // Sprinkled through out the program<BR><BR>
13 Do Something Else<BR><BR>
<BR>
Security Thread<BR>
1 Load security Script into the Script Control<BR>
2 Decrypt the security script<BR>
3 Run the security script<BR>
4 Sleep for a random time A minutes/Hours<BR>
5 If .IsElapsed or .IsPatched or isTimeSetBack then<BR><BR>
  {this block will know if the App has been patched,Time set back, or has just elapsed.}<BR><BR>
6 End Main Program Thread<BR>
7 End Random Timer Thread<BR>
8 End Security Thread<BR>
9 {don't show that we are not registered just stop the program}<BR><BR>
10 End If<BR>
12 End Security Thread<BR>
After all of this Blurb, I come back to the same conclusion we cannot protect a program
from being copied, all we can do is make it hard for the attacker. <BR>
In the above example if the attacker finds all of the 'Start Security Thread' references and NOP's them out then the protection is bypassed.<BR>
I have just gone through Guy's code again and it suffers from the same problems as I have
had with the above idea. All the attacker needs to do is to NOP out the <BR><BR>
'script.ExecuteStatement sCode' line and the program will never get checked. <BR><BR>
The only other change that needs to be made is,<BR><BR>
If Me.Caption = TITLE Then -- changed to -- If Me.Caption <> TITLE Then<BR><BR>
And the program is useable, no need to worry about registration files, or key.<BR><BR>
I have included a compiled patch file to prove the point. With a bit of assembler
knowledge the above is not difficult to do.<BR><BR>
I will still upload this, someone may find it useful and have some more ideas. I hope
that this article spurs on some more discussion in this area.<BR><BR>
 <BR>
Tombr...<BR><BR>

