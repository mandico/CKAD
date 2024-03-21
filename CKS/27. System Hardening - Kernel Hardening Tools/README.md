AppArmor
- Filesystem
- Ref: https://github.com/killer-sh/cks-course-environment/blob/master/course-content/system-hardening/kernel-hardening-tools/apparmor/profile-docker-nginx
- Ref: https://kubernetes.io/docs/tutorials/security/apparmor/

Seccomp: Secure Compute Mode
- Only calls to these allowed:
    - exit()
    - sigreturn()
    - read()
    - write()

- Ref: https://github.com/killer-sh/cks-course-environment/blob/master/course-content/system-hardening/kernel-hardening-tools/seccomp/profile-docker-nginx.json