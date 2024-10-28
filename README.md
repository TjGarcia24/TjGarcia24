#include "SFML/Graphics.hpp"
#include "engine.h"
#include "stdio.h"

using namespace sf;

Engine::Engine (string title) {
	//Fuck you c++
}
Engine::Engine (void) {}

void Engine::init() {
	window.create(sf::VideoMode(640,480), "SFML Test", Style::Close);
	window.setFramerateLimit(60);
	
	tex.loadFromFile("assets/logo.png");
	spr.setTexture(tex, true);
	spr.setPosition(10, 200);
}

void Engine::input(Event e) {
	while (window.pollEvent(e)) {
		if (e.type == Event::Closed) {
			window.close();
		}
		if (e.type == Event::KeyPressed) {
			if (e.key.code == Keyboard::Space) {
				printf("SpaceBar pressed\n");
				window.capture();
			}
			if (e.key.code == Keyboard::Escape) {
				window.close();
			}
		}
	}
}

void Engine::update() {
	spr.setPosition(spr.getPosition().x+5, spr.getPosition().y);

	if (spr.getPosition().x > 640) {
		spr.setPosition(0-252,spr.getPosition().y);
	}
}

void Engine::render() {
	window.clear(Color::Black);
	window.draw(spr);
	window.display();
}
engine.h
#include "SFML/Graphics.hpp"
#include "stdio.h"

using namespace sf;

class Engine {
public:
	//Game Stuff
	Texture tex;
	Sprite spr;

	//Engine Stuff
	RenderWindow window;
	void loop();
	void init();
	void input(Event e);
	void update();
	void render();
};
main.cpp
#include "SFML/Graphics.hpp"
#include "stdio.h"
#include "engine.h"

int main(int argc, char* argv[]) {

	printf("Stuff is happening...\n");
	Engine eng;
	printf("Engine created\n");
	eng.init();
	printf("Engine initialized\n");

	while (eng.window.isOpen()) {
		Event e;
		eng.input(e);
		eng.update();
		eng.render();
	}

	return 0;
}
