---
title:  "[Java] ☕ 스케쥴링 알고리즘 구현"
excerpt: "JAVA CS 지식 관련 정리"
categories:
  - Java
tags:
  - [JUnit, CS, Java]

toc: true
toc_sticky: true
 
date: 2023-11-12
last_modified_at: 2023-11-12
---

## 📖 Process 클래스

하나의 `process`의 정보를 저장하는 `class` 이다.  

```java
public class Process implements Comparable<Process> {
    int processId;
    int arrivalTime;
    int burstTime;
    int temptArrivalTime;
    int temptBurstTime;
    int remainTime;

    int realStartTime;

    public Process(int processId, int arrivalTime, int burstTime) {
        this.processId = processId;
        this.arrivalTime = arrivalTime;
        this.burstTime = burstTime;
    }

    public Process(int processId, int arrivalTime, int burstTime, int temptArrivalTime, int temptBurstTime, int remainTime) {
        this.processId = processId;
        this.arrivalTime = arrivalTime;
        this.burstTime = burstTime;
        this.temptArrivalTime = temptArrivalTime;
        this.temptBurstTime = temptBurstTime;
        this.remainTime = remainTime;
        this.realStartTime = -6666;
    }

    public boolean update(int realStartTime, int temptArrivalTime, int curRemainTime, int timeSlice) {
        if (this.realStartTime == -6666) this.realStartTime = realStartTime;
        this.temptArrivalTime = temptArrivalTime;
        this.remainTime += curRemainTime;
        temptBurstTime -= timeSlice;
        if (temptBurstTime > 0) return true;
        return false;
    }

    @Override
    public int compareTo(Process o) {
        if (this.arrivalTime < o.arrivalTime) return -1;
        else if (this.arrivalTime == o.arrivalTime) return 0;
        else return 1;
    }
}

```

## 📖 FCFS

```java
public class FCFS {
    PriorityQueue<Process> processes;

    public FCFS() {
        processes = new PriorityQueue<>();
    }

    public void setProcesses(int processId, int arrivalTime, int burstTime) {
        processes.add(new Process(processId, arrivalTime, burstTime));
    }

    public void run() {
        int curTime = 0;
        int remainTime = 0;

        System.out.println("============================ FCFS ============================");

        while (!processes.isEmpty()) {
            Process process = processes.poll();

            int curRemainTime = Math.max(0, curTime - process.arrivalTime);
            remainTime += curRemainTime;
            curTime = Math.max(curTime, process.arrivalTime);
            curTime += process.burstTime;

            System.out.println("프로세스 ID: " + process.processId + "\t시작시간: " + process.arrivalTime + "\t수행시간: "
                    + process.burstTime + "\t종료시간: " + curTime + "\t지연시간: " + curRemainTime);
        }

        System.out.println("끝난 시간: " + curTime);
        System.out.println("지연 시간: " + remainTime);
    }
}

```

<br>


## 📖 LIFO

```java
public class LIFO {
    PriorityQueue<Process> processesToRun;
    Stack<Process> processes;

    public LIFO() {
        this.processesToRun = new PriorityQueue<>();
        this.processes = new Stack<>();
    }

    public void setProcesses(int processId, int arrivalTime, int burstTime) {
        processesToRun.add(new Process(processId, arrivalTime, burstTime));
    }

    public void run() {
        int curTime = 0;
        int remainTime = 0;

        System.out.println("============================ LIFO ============================");

        while (!processesToRun.isEmpty()) {
            if (curTime <= processesToRun.peek().arrivalTime) {
                curTime = processesToRun.peek().arrivalTime;
                processes.add(processesToRun.poll());
            }
            while (!processesToRun.isEmpty() && curTime >= processesToRun.peek().arrivalTime) {
                processes.add(processesToRun.poll());
            }


            while (!processes.isEmpty()) {
                Process process = processes.pop();

                int curRemainTime = Math.max(0, curTime - process.arrivalTime);
                remainTime += curRemainTime;
                curTime = Math.max(curTime, process.arrivalTime);
                curTime += process.burstTime;

                System.out.println("프로세스 ID: " + process.processId + "\t시작시간: " + process.arrivalTime + "\t수행시간: "
                        + process.burstTime + "\t종료시간: " + curTime + "\t지연시간: " + curRemainTime);
            }

        }

        System.out.println("끝난 시간: " + curTime);
        System.out.println("지연 시간: " + remainTime);
    }
}

```

<br>

## 📖 RR(Round - Robin)

```java
public class RR {
    int timeSlice;
    PriorityQueue<Process> processesToRun;
    Queue<Process> processes;


    public RR(int timeSlice) {
        this.timeSlice = timeSlice;
        processes = new LinkedList<>();
        processesToRun = new PriorityQueue<>();
    }

    public void setProcesses(int processId, int arrivalTime, int burstTime) {
        processesToRun.add(new Process(processId, arrivalTime, burstTime, arrivalTime, burstTime, 0));
    }

    public void run() {
        int curTime = 0;
        int remainTime = 0;

        System.out.println("==================================== RR ======================================");

        while (!processesToRun.isEmpty() || !processes.isEmpty()) {
            if (processes.isEmpty() && curTime <= processesToRun.peek().temptArrivalTime) {
                curTime = processesToRun.peek().temptArrivalTime;
                processes.add(processesToRun.poll());
            }

            while (!processesToRun.isEmpty() && curTime >= processesToRun.peek().temptArrivalTime) {
                processes.add(processesToRun.poll());
            }

            Process process = processes.poll();


            int curRemainTime = Math.max(0, curTime - process.temptArrivalTime);
            curTime = Math.max(curTime, process.temptArrivalTime);
            curTime += Math.min(process.burstTime, timeSlice);
            if (process.update(curTime - Math.min(process.burstTime, timeSlice), curTime, curRemainTime, timeSlice)) {
                processes.add(process);
            } else {
                remainTime += process.remainTime;
                System.out.println("프로세스 ID: " + process.processId + "\t시작시간: " + process.arrivalTime + "\t실제시작시간: " + process.realStartTime + "\t수행시간: "
                        + process.burstTime + "\t종료시간: " + curTime + "\t지연시간: " + process.remainTime);
            }
        }
        System.out.println("끝난 시간: " + curTime);
        System.out.println("지연 시간: " + remainTime);
    }
}

```

<br>

## 📖 실제 작동

```java
public class main {
    public static void main(String[] args) {
        FCFS fcfs = new FCFS();

        fcfs.setProcesses(1,0,2);
        fcfs.setProcesses(2,2,5);
        fcfs.setProcesses(3,3,1);
        fcfs.setProcesses(4,4,1);

        fcfs.run();

        LIFO lifo = new LIFO();

        lifo.setProcesses(1,0,2);
        lifo.setProcesses(2,2,5);
        lifo.setProcesses(3,3,1);
        lifo.setProcesses(4,4,1);

        lifo.run();

        RR rr = new RR(1);

        rr.setProcesses(1,0,2);
        rr.setProcesses(2,2,5);
        rr.setProcesses(3,3,1);
        rr.setProcesses(4,4,1);

        rr.run();

    }
}
```

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/21f5c264-0389-4414-93c0-bedf46e17280)


<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁