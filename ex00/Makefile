CXX      := c++
CXXFLAGS := -g -MMD -MP -Wall -Wextra -Werror -std=c++98
DFLAGS   := -fsanitize=address -fsanitize=undefined -fsanitize=bounds
INCLUDE  := -I .
NAME     := zombie
SRCS     := main.cpp Zombie.cpp newZombie.cpp randomChump.cpp
OBJS     := $(SRCS:.cpp=.o)
DEPENDS  := $(OBJS:.o=.d)

all: $(NAME)

$(NAME): $(OBJS) $(LIBS)
	$(CXX) -o $@ $^ $(INCLUDE) $(CXXFLAGS) $(if $(DEBUG),$(DFLAGS),)

%.o: %.cpp
	$(CXX) $(CXXFLAGS) $(if $(DEBUG),$(DFLAGS),) $(INCLUDE) -o $@ -c $<

clean:
	$(RM) -r $(OBJS) $(DEPENDS)

fclean: clean
	$(RM) $(NAME)

re: fclean all

debug:
	make DEBUG=1

valgrind: re
	valgrind --leak-check=full --show-leak-kinds=all --track-fds=yes ./$(NAME)

-include $(DEPENDS)

.PHONY: all clean fclean re valgrind lint
