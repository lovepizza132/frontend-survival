# Test Driven Development

1. TDD Cycle

- Red -> 실패하는 테스트 코드를 작성.
      인터페이스와 스펙에 집중
- Green -> 재빨리 테스트를 통과시킨다.
      올바른 방법이 아니어도 좋다.
- Refactor -> 리펙터링을 통해 코드를 올바르게 만든다.
      TDD에서 가장 중요한 부분이지만, 간과될 때가 많다.

- 개별 테스트를 나열하는 방식
      예시
      ```zsh
      test('add', () => {
            expect(add(1, 2)).toBe(3);
      });
      ```

2. BDD

- 주체-행위 중심으로 테스트를 조직화하는 방식.
      `given - when - then`으로 구분

- 예시
      ```zsh
      const context = describe;

      describe('add', () => {
            context('with no argument', () => {
                  it('returns zero', () => {
                        expect(add()).toBe(0);
                  });
            });

            context('with only one number', () => {
                  it('returns the same number', () => {
                        expect(add(1)).toBe(1);
                  });
            });

            context('with two numbers', () => {
                  it('returns sum of two numbers', () => {
                        expect(add(1, 2)).toBe(3);
                  });
            });

            context('with three numbers', () => {
                  it('returns sum of three numbers', () => {
                        expect(add(1, 2, 3)).toBe(6);
                  });
            });
      });
      ```
- jest에서 TypeScript가 작동하도록 jest.config.js 파일 작성
      ```zsh
      module.exports = {
            testEnvironment: 'jsdom',
            setupFilesAfterEnv: [
            '@testing-library/jest-dom/extend-expect',
            ],
            transform: {
            '^.+\\.(t|j)sx?$': ['@swc/jest', {
                  jsc: {
                  parser: {
                  syntax: 'typescript',
                  jsx: true,
                  decorators: true,
                  },
                  transform: {
                  react: {
                        runtime: 'automatic',
                  },
                  },
                  },
            }],
            },
      };
      ```
