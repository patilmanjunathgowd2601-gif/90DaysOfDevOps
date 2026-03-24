# Day 20 – Bash Scripting Challenge: Log Analyzer
## Script Code

```bash
          #!/bin/bash
          # ===============================
          # Log Analyzer Script
          # ===============================
          
          # Task 1: Input Validation
          if [ $# -eq 0 ]; then
              echo " Error: No log file provided."
              echo "Usage: $0 <log_file>"
              exit 1
          fi
          
          LOG_FILE="$1"
          
          if [ ! -f "$LOG_FILE" ]; then
              echo " Error: File does not exist: $LOG_FILE"
              exit 1
          fi
          
          # Date for report
          DATE=$(date +%Y-%m-%d)
          REPORT_FILE="log_report_${DATE}.txt"
          
          echo " Processing log file: $LOG_FILE"
          echo "----------------------------------"
          
          # Task 2: Error Count
          ERROR_COUNT=$(grep -E -c "ERROR|Failed" "$LOG_FILE")
          echo " Total Error Count: $ERROR_COUNT"
          
          # Task 3: Critical Events
          CRITICAL_EVENTS=$(grep -n "CRITICAL" "$LOG_FILE")
          
          echo ""
          echo "--- Critical Events ---"
          if [ -z "$CRITICAL_EVENTS" ]; then
              echo "No critical events found."
          else
          echo "$CRITICAL_EVENTS"
          fi
          
          # Task 4: Top 5 Error Messages
          TOP_ERRORS=$(grep "ERROR" "$LOG_FILE" \
              | awk '{$1=$2=$3=""; print $0}' \
              | sed 's/^ *//' \
              | sort \
              | uniq -c \
              | sort -rn \
              | head -5)
          
          echo ""
          echo "--- Top 5 Error Messages ---"
          echo "$TOP_ERRORS"
          
          # Total lines
          TOTAL_LINES=$(wc -l < "$LOG_FILE")
          
          # Task 5: Generate Report
          {
              echo "===== Log Analysis Report ====="
              echo "Date: $DATE"
              echo "Log File: $LOG_FILE"
              echo "Total Lines: $TOTAL_LINES"
              echo "Total Errors: $ERROR_COUNT"
              echo ""
          
              echo "--- Top 5 Error Messages ---"
              echo "$TOP_ERRORS"
              echo ""
          
              echo "--- Critical Events ---"
              if [ -z "$CRITICAL_EVENTS" ]; then
                  echo "No critical events found."
              else
                  echo "$CRITICAL_EVENTS"
              fi
          } > "$REPORT_FILE"
          
          echo ""
          echo " Report generated: $REPORT_FILE"
          
          # Task 6 : Archive
          ARCHIVE_DIR="archive"
          
          if [ ! -d "$ARCHIVE_DIR" ]; then
              mkdir "$ARCHIVE_DIR"
          fi
          
          mv "$LOG_FILE" "$ARCHIVE_DIR/"
          
          echo " Log file moved to $ARCHIVE_DIR/"
output:
 ./log_analyzer.sh sample_log.log
 Processing log file: sample_log.log
----------------------------------
 Total Error Count: 6

--- Critical Events ---
4:2025-07-29 10:15:23 CRITICAL Disk space below threshold
8:2025-07-29 10:25:00 CRITICAL Database connection lost

--- Top 5 Error Messages ---
      2 Connection timed out
      1 Permission denied
      1 File not found
      1 Disk I/O error

 Report generated: log_report_2026-03-24.txt
 Log file moved to archive/

## Commands
    -grep → search patterns
    -awk → process and clean text
    -sort → organize output
    -uniq -c → count occurrences
    -head → limit results
    -wc -l → count lines
    -mv → move files
    -date → generate timestamp

What I Learned
      -Combining Unix tools (grep, awk, sort) creates powerful pipelines.
      -Text processing is extremely efficient in Bash for log analysis.
      -Input validation is essential for writing reliable scripts.
              
                                                  
