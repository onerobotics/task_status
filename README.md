# TASK_STATUS

KAREL utility to check the status of a task from TPE.

Because there's no other way to check if a task is running
from TPE. This can be a problem if you're counting on a
background task to be running or an asynchronous task to
be not running before firing it off again.

## Usage

    CALL TASK_STATUS('PROGRAM_NAME', outputRegId) ;

| Return Value | Meaning |
| ------------ | ------- |
| -2           | Run request has been accepted |
| -1           | Abort request has been accepted |
| 0            | Task is running |
| 1            | Task is paused |
| 2            | Task is aborted |
| Other        | Refer to Error Code manual |


## Example

    LBL[1] ;
    CALL TASK_STATUS(‘ASYNC_TASK’,1) ;
    IF R[1:TASK STATUS]<>2,JMP LBL[501] ;
    ! task is aborted ;
    RUN ASYNC_TASK ;
    END ;
     ;
    LBL[501] ;
    ! task is still doing something or hung up ;
    JMP LBL[1] ;
