<div align="center">

## RunOnlyOnce: via Mutex\.


</div>

### Description

Code: Another, different, RunOnlyOnce solution.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[David Ward](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/david-ward.md)
**Level**          |Beginner
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |Delphi 5, Delphi 4, Pre Delphi 4
**Category**       |[Windows API Call/ Explanation](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/windows-api-call-explanation__7-39.md)
**World**          |[Delphi](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/delphi.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/david-ward-runonlyonce-via-mutex__7-534/archive/master.zip)





### Source Code

```
So here it is then, a 3 step process.
[1] Put the following function declaration in the INTERFACE section of any unit of your project,
immediately prior to the IMPLEMENTATION section header;
Function AlreadyRunning: Boolean;
[2] and the following function in the IMPLEMENTATION section of that same unit;
Function AlreadyRunning: Boolean;
Var
  MutexHandle: THandle;
Begin
   Result:=False;
   MutexHandle:=CreateMutex(nil,TRUE,'NameofMyProgram-version1.2.3');
   // 'NameofMyProgram-version1.2.3' can be any text string, it just needs to be unique to each program.
   If MutexHandle<>0 then
     If GetLastError=ERROR_ALREADY_EXISTS then
      Result:=True; // Yes, this Mutex does already exist, this program is already running!
end;
[3] Finally, in your Project source file (the .DPR) in the main "Begin ... End." clause do this;
Begin // existing line
 If not AlreadyRunning then
 begin
  // inside here will be ALL the existing code that already was in the main "Begin ... End." clause.
 end;
End. // existing line
```

