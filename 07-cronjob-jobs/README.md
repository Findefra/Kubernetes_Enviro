# 07 - CronJob & Jobs

**Skills demonstrated:** CronJob, Job, concurrency policy, successfulJobsHistoryLimit, backoffLimit, restartPolicy, one-off vs scheduled workloads.

## What this shows

- Scheduled recurring tasks (database backup simulation, report generation, cleanup)
- One-time Jobs for migrations / batch processing
- Proper history limits so completed pods don’t accumulate forever
- Concurrency control (`Forbid` vs `Allow` vs `Replace`)

## Deploy

```bash
kubectl apply -f .
kubectl get cronjob,job,pods -l app=backup
# Force a Job from the CronJob for testing
kubectl create job --from=cronjob/db-backup manual-backup-$(date +%s)
```

## Cleanup

```bash
kubectl delete -f .
```
