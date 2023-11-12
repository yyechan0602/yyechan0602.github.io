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

    public Process(int processId, int arrivalTime, int burstTime) {
        this.processId = processId;
        this.arrivalTime = arrivalTime;
        this.burstTime = burstTime;
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
    PriorityQueue<Process> processes;

    public RR() {
        processes = new PriorityQueue<>();
    }

    public void setProcesses(int processId, int arrivalTime, int burstTime) {
        processes.add(new Process(processId, arrivalTime, burstTime));
    }

    public void run() {
        int curTime = 0;
        int remainTime = 0;

        System.out.println("============================= RR =============================");

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

        RR rr = new RR();

        rr.setProcesses(1,0,2);
        rr.setProcesses(2,2,5);
        rr.setProcesses(3,3,1);
        rr.setProcesses(4,4,1);

        rr.run();

    }
}

```

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁