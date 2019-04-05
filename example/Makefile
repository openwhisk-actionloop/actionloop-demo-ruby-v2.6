IMG=actionloop-demo-ruby-v2.6:latest
ACT=hello-demo-ruby

src.zip:
	zip src.zip main.rb hello.rb

bin.zip: src.zip
	docker run -i $(IMG) -compile main <src.zip >bin.zip

single:
	wsk action update $(ACT) hello.py --docker $(IMG) --main hello

src-zip: src.zip
	wsk action update $(ACT) $< --docker $(IMG)

bin-zip: bin.zip
	wsk action update $(ACT) $< --docker $(IMG)

test:
	wsk action invoke $(ACT) -r
	wsk action invoke $(ACT) -p name Mike -r

.PHONE: single src-zip bin-zip

