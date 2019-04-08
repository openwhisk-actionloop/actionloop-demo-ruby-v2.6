IMG=actionloop-demo-ruby-v2.6:latest
ACT=hello-demo-ruby
PREFIX=docker.io/actionloop

src.zip: main.rb hello.rb
	zip src.zip main.rb hello.rb

bin.zip: src.zip
	docker run -i $(IMG) -compile main <src.zip >bin.zip

test-single:
	wsk action update $(ACT) hello.rb --docker $(PREFIX)/$(IMG) --main hello
	wsk action invoke $(ACT) -r
	wsk action invoke $(ACT) -p name Mike -r

test-src-zip: src.zip
	wsk action update $(ACT) $< --docker $(PREFIX)/$(IMG)
	wsk action invoke $(ACT) -r
	wsk action invoke $(ACT) -p name Mike -r

test-bin-zip: bin.zip
	wsk action update $(ACT) $< --docker $(PREFIX)/$(IMG)
	wsk action invoke $(ACT) -r
	wsk action invoke $(ACT) -p name Mike -r

.PHONE: test-single test-src-zip test-bin-zip

