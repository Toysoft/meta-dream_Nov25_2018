Dreambox BSP layer for:
```
dm500hd - boot status is ?
dm500hdv2 - boot status is ?
dm520 - boot status is ?
dm800se - boot status is ?
dm800sev2 - boot status is ?
dm900 - boot status is ?
dm7020hd - boot status is ok
dm7020hdv2 - boot status is ?
dm8000 - boot status is ?
```
How does it work? Simply with PLi's OE!

Use https://github.com/OpenPLi/openpli-oe-core (develop branch) with Ubuntu 16.04.2 LTS (4.8.0-58 kernel) as your base, Open a terminal inside "openpli-oe-core" folder and enter:
```
rm -rf meta-dream
git clone https://github.com/DMM-PLi/meta-dream.git
```
Now edit the "Makefile" file:
```
$(BBLAYERS):
	[ -d $@ ] || $(MAKE) $(MFLAGS) update

+EXACTNAME = $(MACHINE)
+export EXACTNAME
+ifeq ($(MACHINE),dm7020hdv2)
+MACHINE=dm7020hd
+EXACTNAME=dm7020hdv2
+endif

initialize: init
```
and
```
+	@echo 'export BB_ENV_EXTRAWHITE="MACHINE EXACTNAME"' > $@
+	@echo 'export MACHINE' >> $@
	@echo 'export EXACTNAME' >> $@
```
For latest updates you need to open a terminal inside "meta-dream" folder and enter:
```
git pull origin master
```
each time you do "make update" for the OE.

Experimental machines:
```
dm800 not yet ready for build!
dm820 - not yet ready for build!
dm7080 - not yet ready for build!
```
We're independent so if you think you can help you're welcome to send us merge requests.
