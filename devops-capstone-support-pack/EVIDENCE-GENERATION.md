# Evidence generation (run these in the real lab/project environment)

Replace `/path/to/project` and the service URL as appropriate. These commands produce real output files from your environment. They do not create the screenshots; capture those from GitHub Projects/Kanban, GitHub Actions, the application browser, Kubernetes/OpenShift or Tekton console.

## REST API cURL output files

The starter service exposes POST `/accounts`. Complete and verify the READ, LIST, UPDATE and DELETE routes/tests in the course labs before capturing their outputs. Use your real running service base URL (examples assume `http://localhost:8080`).

```bash
# CREATE — run after the service and database are ready
{ echo '$ curl -i -X POST http://localhost:8080/accounts -H "Content-Type: application/json" -d ...'; curl -i -X POST http://localhost:8080/accounts -H 'Content-Type: application/json' -d '{"name":"Jamie Smith","email":"jamie@example.com","address":"1 Main Street","phone_number":"555-0100"}'; } 2>&1 | tee rest-create-done

# LIST (expected route after you complete the LIST lab)
{ echo '$ curl -i http://localhost:8080/accounts'; curl -i http://localhost:8080/accounts; } 2>&1 | tee rest-list-done

# READ (replace 1 with the real ID returned by CREATE)
{ echo '$ curl -i http://localhost:8080/accounts/1'; curl -i http://localhost:8080/accounts/1; } 2>&1 | tee rest-read-done

# UPDATE (replace 1 with a real ID)
{ echo '$ curl -i -X PUT http://localhost:8080/accounts/1 -H "Content-Type: application/json" -d ...'; curl -i -X PUT http://localhost:8080/accounts/1 -H 'Content-Type: application/json' -d '{"name":"Jamie Smith Updated","email":"jamie@example.com","address":"2 Main Street","phone_number":"555-0100"}'; } 2>&1 | tee rest-update-done

# DELETE (replace 1 with a real ID; capture the actual status/body)
{ echo '$ curl -i -X DELETE http://localhost:8080/accounts/1'; curl -i -X DELETE http://localhost:8080/accounts/1; } 2>&1 | tee rest-delete-done
```

## CI and security tests

```bash
# GitHub CLI must be installed and authenticated; use a real run ID.
gh run list --workflow ci-build.yaml --limit 5
gh run view <RUN_ID> --log 2>&1 | tee ci-workflow-done

# Run after installing Talisman/CORS and completing their tests.
nosetests -vv --with-spec --spec-color --with-coverage --cover-package=service 2>&1 | tee security-headers-done
```

## Browser / Kubernetes / Docker / Tekton

```bash
# Copy actual JSON response from the application's internal browser on port 8080.
# If accessible from the terminal, this records the same endpoint response:
curl -sS http://localhost:8080/ | tee kube-app-output

# Actual local Docker image inventory
docker images | tee kube-images

# Actual Kubernetes resources (run with the lab's correct context/namespace)
kubectl get deployments,pods,replicasets,services -o wide | tee kube-deploy-accounts

# Start the course's actual Tekton pipeline using the parameters from its lab instructions.
# The exact tkn command depends on your pipeline name, repository URL, workspace/PVC and image.
# Save the output from your real run, e.g.:
tkn pipeline start <PIPELINE_NAME> <COURSE_PARAMETERS_AND_WORKSPACES> --showlog 2>&1 | tee pipelinerun.txt
```

For `pipelinerun.txt`, make sure the file includes the complete log output for the actual run. Do not put a made-up “all tests passed” summary in place of the logs.

## Screenshots

Capture screenshots directly from the actual GitHub Project board and deployment/pipeline UI. Use the exact filenames in `SUBMISSION-FILE-MAP.md`. Do not create or submit mockups as evidence.
