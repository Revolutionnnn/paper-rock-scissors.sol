// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract RockPaperScissors {
  // Los posibles movimientos
  enum Move {
    Rock,
    Paper,
    Scissors
  }

  // El movimiento del jugador actual
  Move public currentPlayerMove;

  // El movimiento de la computadora
  Move public computerMove;

  // El ganador del juego
  address public winner;

  event PremioReclamado(address ganador);

  // El constructor
  constructor() {
    currentPlayerMove = Move.Rock;
    computerMove = Move.Rock;
    winner = address(0);
  }

  // La función para realizar un movimiento y jugar el juego
  function makeMove(Move move) public {
    currentPlayerMove = move;

    // Generar el movimiento de la computadora
    computerMove = generateComputerMove();

    // Determinar el ganador
    address gameWinner = determineWinner();

    // Si el jugador ganó, puede reclamar el premio
    if (gameWinner == msg.sender) {
      winner = gameWinner;
      claimPrize();
    }
  }

  // La función para generar el movimiento de la computadora
  function generateComputerMove() private view returns (Move) {
    uint8 randomNumber = uint8(uint256(keccak256(abi.encodePacked(block.timestamp, block.difficulty))) % 3);
    if (randomNumber == 0) {
      return Move.Rock;
    } else if (randomNumber == 1) {
      return Move.Paper;
    } else {
      return Move.Scissors;
    }
  }

  // La función para determinar el ganador
  function determineWinner() private view returns (address) {
    if (currentPlayerMove == computerMove) {
      return address(0);
    } else if (currentPlayerMove == Move.Rock && computerMove == Move.Scissors) {
      return msg.sender;
    } else if (currentPlayerMove == Move.Paper && computerMove == Move.Rock) {
      return msg.sender;
    } else if (currentPlayerMove == Move.Scissors && computerMove == Move.Paper) {
      return msg.sender;
    } else {
      return address(0);
    }
  }

  // La función para reclamar el premio
  function claimPrize() public {
    require(winner == msg.sender, "Solo el ganador puede reclamar el premio");
    emit PremioReclamado(winner);
  }
}
