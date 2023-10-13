# SonarQube 指标


SonarQube 指标

<!--more-->

## SonarQube 指标

|name                                      | val_type | description  |
|------------------------------------------|----------|--------------|
| lines                                    | INT      | Lines  |
| generated_lines                          | INT      | Number of generated lines  |
| ncloc                                    | INT      | Non commenting lines of code  |
| new_lines                                | INT      | New lines  |
| ncloc_language_distribution              | DATA     | Non Commenting Lines of Code Distributed By Language  |
| generated_ncloc                          | INT      | Generated non Commenting Lines of Code  |
| classes                                  | INT      | Classes  |
| files                                    | INT      | Number of files  |
| directories                              | INT      | Directories  |
| functions                                | INT      | Functions  |
| statements                               | INT      | Number of statements  |
| public_api                               | INT      | Public API  |
| projects                                 | INT      | Number of projects  |
| comment_lines                            | INT      | Number of comment lines  |
| comment_lines_density                    | PERCENT  | Comments balanced by ncloc + comment lines  |
| public_documented_api_density            | PERCENT  | Public documented classes and functions balanced by ncloc  |
| public_undocumented_api                  | INT      | Public undocumented classes, functions and variables  |
| commented_out_code_lines                 | INT      | Commented lines of code  |
| complexity                               | INT      | Cyclomatic complexity  |
| file_complexity                          | FLOAT    | Complexity average by file  |
| complexity_in_classes                    | INT      | Cyclomatic complexity in classes  |
| class_complexity                         | FLOAT    | Complexity average by class  |
| complexity_in_functions                  | INT      | Cyclomatic complexity in functions  |
| function_complexity                      | FLOAT    | Complexity average by function  |
| class_complexity_distribution            | DISTRIB  | Classes distribution /complexity  |
| function_complexity_distribution         | DISTRIB  | Functions distribution /complexity  |
| file_complexity_distribution             | DISTRIB  | Files distribution /complexity  |
| cognitive_complexity                     | INT      | Cognitive complexity  |
| tests                                    | INT      | Number of unit tests  |
| test_execution_time                      | MILLISEC | Execution duration of unit tests  |
| test_errors                              | INT      | Number of unit test errors  |
| skipped_tests                            | INT      | Number of skipped unit tests  |
| test_failures                            | INT      | Number of unit test failures  |
| test_success_density                     | PERCENT  | Density of successful unit tests  |
| test_data                                | DATA     | Unit tests details  |
| coverage                                 | PERCENT  | Coverage by tests  |
| new_coverage                             | PERCENT  | Coverage of new/changed code  |
| lines_to_cover                           | INT      | Lines to cover  |
| new_lines_to_cover                       | INT      | Lines to cover on new code  |
| uncovered_lines                          | INT      | Uncovered lines  |
| new_uncovered_lines                      | INT      | Uncovered lines on new code  |
| line_coverage                            | PERCENT  | Line coverage  |
| new_line_coverage                        | PERCENT  | Line coverage of added/changed code  |
| coverage_line_hits_data                  | DATA     | Coverage hits by line  |
| conditions_to_cover                      | INT      | Conditions to cover  |
| new_conditions_to_cover                  | INT      | Conditions to cover on new code  |
| uncovered_conditions                     | INT      | Uncovered conditions  |
| new_uncovered_conditions                 | INT      | Uncovered conditions on new code  |
| branch_coverage                          | PERCENT  | Condition coverage  |
| new_branch_coverage                      | PERCENT  | Condition coverage of new/changed code  |
| conditions_by_line                       | DATA     | Conditions by line  |
| covered_conditions_by_line               | DATA     | Covered conditions by line  |
| it_coverage                              | PERCENT  | Integration tests coverage  |
| new_it_coverage                          | PERCENT  | Integration tests coverage of new/changed code  |
| it_lines_to_cover                        | INT      | Lines to cover by Integration Tests  |
| new_it_lines_to_cover                    | INT      | Lines to cover on new code by integration tests  |
| it_uncovered_lines                       | INT      | Uncovered lines by integration tests  |
| new_it_uncovered_lines                   | INT      | New lines that are not covered by integration tests  |
| it_line_coverage                         | PERCENT  | Line coverage by integration tests  |
| new_it_line_coverage                     | PERCENT  | Integration tests line coverage of added/changed code  |
| it_coverage_line_hits_data               | DATA     | Coverage hits by line by integration tests  |
| it_conditions_to_cover                   | INT      | Integration Tests conditions to cover  |
| new_it_conditions_to_cover               | INT      | Branches to cover by Integration Tests on New Code  |
| it_uncovered_conditions                  | INT      | Uncovered conditions by integration tests  |
| new_it_uncovered_conditions              | INT      | New conditions that are not covered by integration tests  |
| it_branch_coverage                       | PERCENT  | Condition coverage by integration tests  |
| new_it_branch_coverage                   | PERCENT  | Integration tests condition coverage of new/changed code  |
| it_conditions_by_line                    | DATA     | IT conditions by line  |
| it_covered_conditions_by_line            | DATA     | IT covered conditions by line  |
| overall_coverage                         | PERCENT  | Overall test coverage  |
| new_overall_coverage                     | PERCENT  | Overall coverage of new/changed code  |
| overall_lines_to_cover                   | INT      | Overall lines to cover by all tests  |
| new_overall_lines_to_cover               | INT      | New lines to cover by all tests  |
| overall_uncovered_lines                  | INT      | Uncovered lines by all tests  |
| new_overall_uncovered_lines              | INT      | New lines that are not covered by any tests  |
| overall_line_coverage                    | PERCENT  | Line coverage by all tests  |
| new_overall_line_coverage                | PERCENT  | Line coverage of added/changed code by all tests  |
| overall_coverage_line_hits_data          | DATA     | Coverage hits by all tests and by line  |
| overall_conditions_to_cover              | INT      | Branches to cover by all tests  |
| new_overall_conditions_to_cover          | INT      | New branches to cover by all tests  |
| overall_uncovered_conditions             | INT      | Uncovered conditions by all tests  |
| new_overall_uncovered_conditions         | INT      | New conditions that are not covered by any test  |
| overall_branch_coverage                  | PERCENT  | Condition coverage by all tests  |
| new_overall_branch_coverage              | PERCENT  | Condition coverage of new/changed code by all tests  |
| overall_conditions_by_line               | DATA     | Overall conditions by all tests and by line  |
| overall_covered_conditions_by_line       | DATA     | Overall covered conditions by all tests and by line  |
| duplicated_lines                         | INT      | Duplicated lines  |
| new_duplicated_lines                     | INT      | Duplicated Lines on New Code  |
| duplicated_blocks                        | INT      | Duplicated blocks  |
| new_duplicated_blocks                    | INT      | Duplicated blocks on new code  |
| duplicated_files                         | INT      | Duplicated files  |
| duplicated_lines_density                 | PERCENT  | Duplicated lines balanced by statements  |
| new_duplicated_lines_density             | PERCENT  | Duplicated lines on new code balanced by statements  |
| duplications_data                        | DATA     | Duplications details  |
| violations                               | INT      | Issues  |
| blocker_violations                       | INT      | Blocker issues  |
| critical_violations                      | INT      | Critical issues  |
| major_violations                         | INT      | Major issues  |
| minor_violations                         | INT      | Minor issues  |
| info_violations                          | INT      | Info issues  |
| new_violations                           | INT      | New issues  |
| new_blocker_violations                   | INT      | New Blocker issues  |
| new_critical_violations                  | INT      | New Critical issues  |
| new_major_violations                     | INT      | New Major issues  |
| new_minor_violations                     | INT      | New Minor issues  |
| new_info_violations                      | INT      | New Info issues  |
| false_positive_issues                    | INT      | False positive issues  |
| wont_fix_issues                          | INT      | Won't fix issues  |
| open_issues                              | INT      | Open issues  |
| reopened_issues                          | INT      | Reopened issues  |
| confirmed_issues                         | INT      | Confirmed issues  |
| code_smells                              | INT      | Code Smells  |
| new_code_smells                          | INT      | New Code Smells  |
| bugs                                     | INT      | Bugs  |
| new_bugs                                 | INT      | New Bugs  |
| vulnerabilities                          | INT      | Vulnerabilities  |
| new_vulnerabilities                      | INT      | New Vulnerabilities  |
| sqale_index                              | WORK_DUR | Total effort (in days) to fix all the issues on the component and therefore to comply to all the requirements.  |
| new_technical_debt                       | WORK_DUR | Added technical debt  |
| sqale_rating                             | RATING   | A-to-E rating based on the technical debt ratio  |
| new_maintainability_rating               | RATING   | Maintainability rating on new code  |
| development_cost                         | STRING   | Development cost  |
| new_development_cost                     | STRING   | Development cost on new code  |
| sqale_debt_ratio                         | PERCENT  | Ratio of the actual technical debt compared to the estimated cost to develop the whole source code from scratch |
| new_sqale_debt_ratio                     | PERCENT  | Technical Debt Ratio of new/changed code.  |
| effort_to_reach_maintainability_rating_a | WORK_DUR | Effort to reach maintainability rating A  |
| reliability_remediation_effort           | WORK_DUR | Reliability Remediation Effort  |
| new_reliability_remediation_effort       | WORK_DUR | Reliability remediation effort on new code  |
| reliability_rating                       | RATING   | Reliability rating  |
| new_reliability_rating                   | RATING   | Reliability rating on new code  |
| security_remediation_effort              | WORK_DUR | Security remediation effort  |
| new_security_remediation_effort          | WORK_DUR | Security remediation effort on new code  |
| security_rating                          | RATING   | Security rating  |
| new_security_rating                      | RATING   | Security rating on new code  |
| ncloc_data                               | DATA     | NULL  |
| comment_lines_data                       | DATA     | NULL  |
| executable_lines_data                    | DATA     | NULL  |
| alert_status                             | LEVEL    | The project status with regard to its quality gate.  |
| quality_gate_details                     | DATA     | The project detailed status with regard to its quality gate  |
| quality_profiles                         | DATA     | Details of quality profiles used during analysis  |
| last_commit_date                         | MILLISEC | NULL  |
| burned_budget                            | FLOAT    | NULL  |
| business_value                           | FLOAT    | NULL  |
| team_size                                | INT      | NULL  |
| sonarjava_feedback                       | DATA     | NULL  |

转自 https://blog.csdn.net/lxlmycsdnfree/article/details/88681918


---

> 作者: [张大锅](https://zhang-weiming.github.io/)  
> URL: https://zhang-weiming.github.io/post/sonarqube/metrics/  

