#! /usr/bin/env escript
% vi: ft=erlang

% for erlang practice & ease of visual inspection, represent stacks as lists of
% atoms rather than using numbers

seq(A, B) when B < A -> [];
seq(A, B) -> lists:seq(A, B).

stacks(L, _Min) when length(L) < 2 -> [];
stacks(L, _Min) when length(L) == 2 -> [[L]];
stacks(L, Min) ->
	Split = fun(N) -> tuple_to_list(lists:split(N, L)) end,
	Recurse = fun([H, T]) -> lists:map(fun(X) -> [H] ++ X end, stacks(T, length(H))) end,
	[[ L ]] ++ lists:flatmap(Recurse, lists:map(Split, seq(Min, trunc(length(L) / 2)))).

stacks(L) ->
	lists:map(fun erlang:list_to_tuple/1, stacks(L, 2)).

print_solutions([], _N) -> ok;
print_solutions([H|T], N) ->
	io:format("solution ~p: ~p~n", [N, H]),
	print_solutions(T, N+1).

print_solutions(L) ->
	print_solutions(L, 1).

l_to_n([]) -> [];
l_to_n([H|T]) ->
	lists:sort([ list_to_tuple(lists:sort(lists:map(fun erlang:length/1, tuple_to_list(H)))) | l_to_n(T) ]).

num_duplicates(L) ->
	length(lists:usort(L)) - length(L).

pennies(N) ->
	io:format("N: ~p~n", [N]),
	Input = lists:duplicate(N, x),
	stacks(Input).

pennies(visual, N) ->
	Solutions = pennies(N),
	io:format("~p solutions:~n", [length(Solutions)]),
	Solutions;
pennies(numeric, N) ->
	Solutions = l_to_n(pennies(N)),
	io:format("~p solutions (~p dups):~n", [length(Solutions), num_duplicates(Solutions)]),
	Solutions.

parse_argv([N, Oformat]) ->
	{ list_to_integer(N), list_to_atom(Oformat) };
parse_argv([N]) ->
	{ list_to_integer(N), visual }.

main(Argv) ->
	{ N, Oformat } = parse_argv(Argv),
	Solutions = pennies(Oformat, N),
	print_solutions(Solutions),
	timer:sleep(100).	% hack to stop escript from truncating output
