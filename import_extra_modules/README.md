# Importing extra modules
This was discovered when trying to cleanup imports in a django project to meet pep8 standards. During the cleanup I decided to reduce number of import lines and instead of using a from module import submodule I simply did import module. Then in code I tried to use module.submodule... to use the utility function I wanted.
